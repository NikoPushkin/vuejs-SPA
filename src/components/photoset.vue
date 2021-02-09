<template>
    <div class="photosets-container">
      <div ref='titlesPart' class="photoset-titles">
        <button class='photoset-btn btn-class' @click='openSidebar(service.type)' :key='service.id' v-for='service in services'>{{ service.type }}</button>
        <button class='photoset-btn btn-class' @click='openPreset'>Floral shock</button>
      </div>

      <div :ref='service.type' class="photoset-description" id='photoset-sidebar' :key='service.id' v-for='service in services'>
        <div :ref='"content-"+service.type' class="sidebar-content">
            <div class="close-btn-box">
              <span class='close-btn hover-transform-btn' @click='closeSidebar(service.type)'><i class="fas fa-times"></i></span>
            </div>

            <span>{{ service.description }}</span>
            <span class='price-span'>{{ service.price }} &#8381;</span>
            <b-form-input required type="text" placeholder="Как Вас зовут?"></b-form-input>
            <b-form-input required class='mt-2' type="email" placeholder="Укажите email для связи с Вами"></b-form-input>
            <button class='send-btn btn-class hover-transform-btn' style='height: 50px; width: 100%; margin-top: 10px;'>Отправить</button>
        </div>
      </div>
      <div ref='preset' class="preset-bar">
        <div class="close-btn-box">
          <span class='close-btn hover-transform-btn' @click='closePreset'><i class="fas fa-times"></i></span>
        </div>
        <div class="right-description-box">
          <p class='preset-title'>Коллекция Авторских пресетов</p>
          <p class='preset-name'>«FLORAL SHOCK»</p>
          <div class="preset-description">
            <p><b>В коллекцию включено: </b>8 пресетов для Adobe Lightroom + Lightroom Mobile</p>
            <p><b>Пресеты в 2х форматах: </b>.xmp, .dng;</p>
            <p>Дополнительно вы получите подробную инструкцию по установке как для компьютерной версии так и для мобильной.</p>
            <p>ВНИМАНИЕ: При использовании пресетов возможно потребуется редактирование экспозиции, баланса белого или контрастности отдельно для каждого снимка.</p>
            <p class='preset-price'>Стоимость: 1500&#8381;</p>
          </div>
        </div>
        <div class="demonstration-image-box" ref='presetExamplesBox' v-b-modal.modal-1>
          <div class="">
            <img src="/images/preset1.jpg" alt="">
            <b-modal class='preset-modal' hide-footer centered size='l' id="modal-1">
              <swiper ref='modalSwiperRef' class="swiper" :options="swiperOption">
                <swiper-slide v-for='presetImage in modalSwiper' :key='presetImage.id'>
                    <img class='modal-swiper-image' :src="presetImage">
                </swiper-slide>
                <div class="swiper-button-prev" @click='prevModalImage' slot="button-prev"></div>
                <div class="swiper-button-next" @click='nextModalImage' slot="button-next"></div>
              </swiper>
            </b-modal>
          </div>
          <div class="">
            <img src="/images/presetcover.jpg" alt="">
          </div>
          <div class="">
            <img src="/images/preset3.jpg" alt="">
          </div>
          <div class="">
            <img src="/images/preset4.jpg" alt="">
          </div>
        </div>
      </div>
    </div>

</template>

<script>
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
import 'swiper/swiper-bundle.css'

export default {
  name: 'photoset',
  components: {
    Swiper,
    SwiperSlide
  },
  data() {
    return {
      services: {},
      modalSwiper:  [
          "/images/preset1.jpg",
          "/images/preset3.jpg",
          "/images/preset4.jpg",
          ],
      swiperOption: {
        slidesPerView: 1,
        spaceBetween: 30,
        loop: true,
      }
    }
  },

  props: {
  },

  async created() {
    await this.getPhotosetsDescriptions()
  },

  methods: {
    nextModalImage() {
      this.$refs.modalSwiperRef.$swiper.slideNext()
    },
    prevModalImage() {
      this.$refs.modalSwiperRef.$swiper.slidePrev()
    },

    // close opened window if another one is opening
    closeOpenedDescription() {
      for (let ref in this.$refs) {
        try {
          let refItemStyle = this.$refs[ref][0].style;
          refItemStyle.opacity='0';
          refItemStyle.pointerEvents = 'none'
        } catch { continue }
      }
    },

    openPreset() {
      this.closeOpenedDescription();
      this.$refs.titlesPart.style.display = 'none'

      this.$refs['preset'].style.opacity = '1';
      this.$refs['preset'].style.pointerEvents = 'all';
      if (window.screen.width < 1140) {
        this.$refs['presetExamplesBox'].style.pointerEvents = 'all';
      }
    },

    closePreset() {
      this.$refs.titlesPart.style.width = '100%';
      this.$refs.titlesPart.style.display = 'flex'
      this.$refs['preset'].style.opacity = '0';
      this.$refs['preset'].style.pointerEvents = 'none';
      this.$refs['presetExamplesBox'].style.pointerEvents = 'none'
    },

    openSidebar(photosetType) {
      this.closeOpenedDescription();
      // move photoset-titles to the left side when description window is opened
      this.$refs.titlesPart.style.width = '50%';

      // opens fullscreen description if screen size is small
      if (window.screen.width < 950) {
        this.$refs.titlesPart.style.display = 'none'
      }

      // show description window
      this.$refs[`${photosetType}`][0].style.opacity = '1';
      this.$refs[`content-${photosetType}`][0].style.opacity = '1';
      this.$refs[`content-${photosetType}`][0].style.pointerEvents = 'all';

    },
    closeSidebar(photosetType) {
      // move photoset-titles to the center side when description window is opened
      this.$refs.titlesPart.style.width = '100%';

      if (window.screen.width < 950) {
        this.$refs.titlesPart.style.display = 'flex'
      }
      // hide description window
      this.$refs[`${photosetType}`][0].style.opacity = '0'
      this.$refs[`content-${photosetType}`][0].style.opacity = '0';
      this.$refs[`content-${photosetType}`][0].style.pointerEvents = 'none';
    },

    async getPhotosetsDescriptions() {
      let response = await fetch('http://127.0.0.1:8000/api/get-descriptions');
      if (response.ok) {
        let json = await response.json();
        this.services = json;
      } else {
        console.log('Error' + response.status);
        return;
      }
    },
  }
}
</script>

<style media="screen">
#modal-1 div {
  background: none !important;
  border: none !important
}
#modal-1 header {
  border: none !important;
  padding-top: 1rem ;
  padding-right: 1rem ;
  padding-bottom: 0 ;
  padding-left: 1rem
}

#modal-1 button {
  color: white;
  outline: none
}
.modal-swiper-image {
  width: 100%
}

.course-sect {
  background-color: white !important;
  height: 90%;
  margin-top: 5vh;
}

.photosets-container {
  overflow: hidden;
  position: relative;
  display: flex;
  flex-direction: row;
  width: 90%;
  margin-left: 5%;
  top: 5vh;
  height: 90%;
  background-size: cover;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), url('/images/background2.jpg');
}

.photoset-titles {
  display: flex;
  flex-direction: column;
  width: 100%;
  heigth: 100%;
  justify-content: center;
  align-items: center;
  transition: 0.2s
}

.photoset-btn {
  margin-bottom: 5vh;
  width: 350px;
  font-size: 1.1rem;
  letter-spacing: 3px;
  color: white;
  font-weight: bold;
  text-transform: uppercase;
}

.photoset-btn:focus {
  background: linear-gradient(to right, rgba(85, 85, 85, 0.2), rgba(0, 0, 0, 0.5));
}

.photoset-description {
  position: absolute;
  width: 50%;
  height: 100%;
  transition: all 0.5s;
  right: 0 !important;
  left: auto;
  opacity: 0;
  background: linear-gradient(to bottom, rgba(45, 45, 45, 0.2), rgba(0, 0, 0, 0.5));
  display: flex;
  justify-content: center;
  pointer-events: none;
}

.preset-bar {
  position: absolute;
  width: 100%;
  height: 90vh;
  transition: all 0.5s;
  opacity: 0;
  background-color: white;
  display: grid;
  align-content: center;
  grid-template-columns: 50% 50%;
  grid-template-rows: 100%;
  grid-template-areas:
    "demonstration-image-box right-description-box";
  pointer-events: none;
  background: linear-gradient(to left, rgba(250, 250, 250, 1), rgba(230, 230, 230, 1));
}

.right-description-box {
  padding: 0 3vw;
  color: black;
  grid-area: right-description-box;
  display: grid;
  align-content: center;
}

.demonstration-image-box {
  grid-area: demonstration-image-box;
  display: grid;
  grid-template-columns: 20vw 20vw;
  grid-template-rows: 20vw 20vw;
  align-content: center;
  justify-content: center;
  pointer-events: none;
  border: none;
  outline: none
}

.demonstration-image-box div {
  width: 20vw;
  height: 20vw;
  display: grid;
  justify-content: center;
  align-content: center;
}
.demonstration-image-box img {
  clip-path: inset(0 0 0 0);
  width: 96%;
}

.preset-title {
  letter-spacing: 4px;
  font-weight: bold;
  font-size: 2vh;
  text-align: center;
  margin-bottom: 0
}
.preset-name {
  letter-spacing: 4px;
  font-weight: bold;
  font-size: 2vh;
  text-align: center;
}

.preset-description {
  letter-spacing: 2px;
  font-size: 1.6vh;
  text-align: justify;
}

.preset-price {
  color: #777;
  font-size: 2vh;
  text-align: center;
}

@media screen and (max-width: 1140px) {
  .preset-bar {
    background: linear-gradient(to bottom, rgba(250, 250, 250, 1), rgba(230, 230, 230, 1));
    grid-template-columns: 100%;
    grid-template-rows: 70% 15%;
    grid-template-areas:
      "right-description-box"
      "demonstration-image-box";
    align-content: flex-start;
  }

  .right-description-box {
    align-content: center;
  }

  .demonstration-image-box {
    grid-area: demonstration-image-box;
    display: grid;
    grid-template-columns: 20vw 20vw 20vw 20vw;
    grid-template-rows: auto;
    justify-content: space-around;
    padding: 0 10px;
  }
}

@media screen and (max-width: 950px) {
  .photoset-description {
    width:100%;
    background: linear-gradient(to bottom, rgba(45, 45, 45, 0.5), rgba(0, 0, 0, 0.9));
  }
}

.sidebar-content {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: justify;
  width: 80%;
  font-weight: bold;
  color: white;
  opacity: 0;
}


.sidebar-content > span {
  margin-bottom: 20px;
  font-size: 20px;
}

@media screen and (max-width: 500px) {
  .price-span {
    font-size: 18px
  }
  .sidebar-content > span {
    font-size: 14px;
    margin-bottom: 8px;

  }

  .photoset-btn {
    margin-bottom: 5vh;
    width: 350px;
    font-size: 0.8rem;
    letter-spacing: 3px;
    color: white;
    font-weight: bold;
    text-transform: uppercase;
  }
}

.price-span {
  color: #777;
  font-size: 25px
}

.send-btn {
  color: white;
  font-weight: bold;
  text-transform: uppercase;
}

.close-sidebar-btn {
  cursor: pointer;
}
</style>

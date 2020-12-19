<template>
  <section id='CЪЕМКА'>
    <div class='photoset-cont' ref='photocont'>
      <div class="button-bar" :ref='"button-"+index' :key='service.id' v-for='(service, index) in services'>
        <button :class='"button-"+index' @click='collapseVisibilityControl("collapse-", index)'
                >
          {{ Object.values(service)[0] }}
        </button>
        <b-collapse :class='"collapse-"+index' v-model='collapseVisibility["collapse-"+index]'
                    style='color: black;' class="mt-2"
                    >
          <b-card style="max-width: 100%" class='pl-0'>
            <p class='about-photoset'>
              {{ Object.values(service)[1] }}

            </p>
            <div class='job-title'
              >
              {{ Object.values(service)[2] }}&#8381;
              <div class='book-service'
                @click='collapseVisibilityControl("subCollapse-", index)'
                >
                <i class="fas fa-feather-alt book-icon"></i>
              </div>
            </div>
            <b-collapse v-model='collapseVisibility["subCollapse-"+index]' class="mt-2">
              <b-form-input required type="text" placeholder="Как Вас зовут?"></b-form-input>
              <b-form-input required class='mt-2' type="email" placeholder="Укажите email для связи с Вами"></b-form-input>
              <button style='height: 50px; width: 100%; margin-top: 10px;'>Отправить</button>
            </b-collapse>
          </b-card>
        </b-collapse>
      </div>
    </div>

    <div class='mobile-photoset-container'>
      <swiper ref='mySwiperRef' class="photoset-swiper" :options="swiperOption">
        <swiper-slide class='mobile-photoset-slide' v-for='(service, index) in services' :key='service.id'>
          <div class="mobile-service-container">
            <b-card class='mobile-photoset-card'>
                <p>
                  <span>{{ Object.values(service)[0] }}</span>
                  <span>{{ Object.values(service)[1] }}</span>
                </p>


              <b-card-text class='mobile-job-title'
                >
                {{ Object.values(service)[2] }}&#8381;
                <div class='book-service'
                  @click='collapseVisibilityControl("subCollapse-", index)'
                  >
                  <i class="fas fa-feather-alt book-icon"></i>
                </div>
              </b-card-text>
              <b-collapse v-model='collapseVisibility["subCollapse-"+index]' class="mt-2">
                <b-form-input required type="text" placeholder="Как Вас зовут?"></b-form-input>
                <b-form-input required class='mt-2' type="email" placeholder="Укажите email для связи с Вами"></b-form-input>
                <button style='height: 2rem; width: 100%; margin-top: 0.5rem;'>Отправить</button>
              </b-collapse>
            </b-card>
          </div>
          <!-- <div> -->
            <!-- <img ref='sliderImage' :src="image"> -->
          <!-- </div> -->
        </swiper-slide>
        <!-- <div class="swiper-pagination" slot="pagination"></div> -->
        <div class="swiper-button-prev" @click='prev' slot="button-prev"></div>
        <div class="swiper-button-next" @click='next' slot="button-next"></div>
      </swiper>
    </div>
  </section>
</template>

<script>
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'

import 'swiper/swiper-bundle.css'

export default {
  name: 'PhotoSet',
  components: {
    Swiper,
    SwiperSlide
  },
  props: {
    csrfToken: String
  },
  data() {
    return {
      services: {},
      collapseVisibility: {
                  'collapse-0': false,
                  'collapse-1': false,
                  'collapse-2': false,
                  'subCollapse-0': false,
                  'subCollapse-1': false,
                  'subCollapse-2': false,
                },
      emailForm: {
        message_name: 'ololololo',
        message_email: 'nikopushkin1@gmail.com',
        message: 'hehehehehehe'
      },
      swiperOption: {
        slidesPerView: 1,
        slidesPerGroup: 1,
        spaceBetween: 30,
        loop: true,
      }
    }
  },

  created() {
    this.getPhotosetsDescriptions();
    this.sendEmail(this.csrfToken);
  },

  methods: {
    collapseVisibilityControl(collapse, id) {
      // closes collapse and moves button to the section center
      if (this.collapseVisibility[`${collapse}${id}`]) {
        this.collapseVisibility[`${collapse}${id}`] = !this.collapseVisibility[`${collapse}${id}`]
        if (collapse != 'subCollapse-') {
          this.$refs[`button-${id}`][0].style.marginTop = '20%'
        }
      // открывает коллапс и смещает кнопку к потолку
      // } else {
      //   // let stay opened only one collapse at the moment
      //   if (this.$refs['photocont'].clientWidth < 1200 && collapse != 'subCollapse-') {
      //     for (let i in this.collapseVisibility) {
      //       this.collapseVisibility[i] = false
      //     }
      //     this.collapseVisibility[`${collapse}${id}`] = !this.collapseVisibility[`${collapse}${id}`]
      //     // it is possible to open multiple collapses
        } else {
          this.collapseVisibility[`${collapse}${id}`] = !this.collapseVisibility[`${collapse}${id}`]
          this.$refs[`button-${id}`][0].style.marginTop = '10vh'
      }
      // }

    },
    // get services descriptions
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

    async sendEmail(token) {
      console.log('TOKEN: ', token);
      var request = new Request(
              'http://127.0.0.1:8000/api/send-email',
              {headers: {'X-CSRFToken': token }}
            );
      let data = this.emailForm;
      let response = await fetch(request, {
                                  method: 'POST',
                                  body: JSON.stringify(data),
                                  credentials: 'include'
                                });
      return response;
    },

    next() {
      this.$refs.mySwiperRef.$swiper.slideNext()
    },
    prev() {
      this.$refs.mySwiperRef.$swiper.slidePrev()
    },
  }
}
</script>

<style media="screen">
.mobile-photoset-container {
  display: none
}

.job-title {
  text-align: center;
  color: #777;
  font-size: 1.2rem;
  font-weight: 300;
  margin-bottom: 1rem
}

.about {
  margin-top: 0;
  font-size: 1rem;
  color: #333;
}

.photoset-cont {
  width: 90%;
  margin-left: 5%;
  height: 100vh;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  text-align: justify;
}

.button-bar {
  width: 33% !important;
  margin-top: 20%;
  transition: .4s;
}

.button-bar button {
  background-color: white;
  /* background: rgba(0, 0, 0, 0.5); */
  letter-spacing: 1px;
  position: sticky;
  clip-path: polygon(40 0 0 0);
  width: 100%;
  height: 3rem;
  color: black;
  font-size: 1.3rem;
  outline: none;
  border: none;
  transition: .4s
}

.book-service {
  display: inline-block;
  color: blue;
  padding: 0px 10px;
  transition: .4s;
  outline: none
}

.book-service:hover {
  transform: scale(1.4, 1.4);
  cursor: pointer;
}

input[type="button"]::-moz-focus-inner {
   border: 0;
}

button:focus {
  outline: none !important;
}

/* .button-1, .collapse-1 {
  margin-right: 5%;
  margin-left: 5%
} */

.button-bar button:hover {
  transform: scale(1.1, 1.1);
}

@media screen and (max-width: 1200px){
  .photoset-cont {
    display: none
  }

  .mobile-photoset-container {
    display: flex;
    height: 100vh;
    width: 100%;
    justify-content: center;
    align-items: center;
  }

  .photoset-swiper {
    width: 90%;
    height: 100vh;
  }

  .mobile-photoset-slide {
    display: flex;
    height: 100vh;
    align-items: center;
    text-align: justify;
  }

  .mobile-photoset-card {
    max-height: 80vh;
  }

  .card-body {
    padding: 1rem !important
  }

  .mobile-about-photoset {
    margin: 0
  }

  .mobile-photoset-card span {
    display: block;
  }

  .mobile-photoset-card span:first-of-type {
    margin-bottom: -10px;
    letter-spacing: 3px;
    font-size: 0.9em;
    font-weight: bold;
    padding-bottom: 1rem;
    text-align: center;
  }

  .mobile-photoset-card span:last-of-type {
    margin-bottom: -10px;
    letter-spacing: 2px;
    font-size: 0.8em;
  }

  .mobile-job-title {
    margin-top: 1rem !important;
    margin-bottom: 0;
    text-align: center;
  }

  .mobile-photoset-container button {
    background-color: white;
    /* background: rgba(0, 0, 0, 0.5); */
    letter-spacing: 1px;
    position: sticky;
    clip-path: polygon(40 0 0 0);
    width: 100%;
    height: 3rem;
    color: black;
    font-size: 1.3rem;
    outline: none;
    border: none;
    transition: .4s
  }
}
</style>

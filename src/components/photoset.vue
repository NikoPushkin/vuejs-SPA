<template>
  <section id='ОБУЧЕНИЕ' class='course-sect'>
    <div class="photosets-container">
      <div ref='titlesPart' class="photoset-titles">
        <button class='photoset-btn' @click='openSidebar(service.type)' :key='service.id' v-for='service in services'>{{ service.type }}</button>
      </div>

      <div :ref='service.type' class="photoset-description" id='photoset-sidebar' :key='service.id' v-for='service in services'>
        <div :ref='"content-"+service.type' class="sidebar-content">
            <span class='close-sidebar-btn' @click='closeSidebar(service.type)'><i class="fas fa-times"></i></span>
            <span>{{ service.description }}</span>
            <span class='price-span'>{{ service.price }} &#8381;</span>
            <b-form-input required type="text" placeholder="Как Вас зовут?"></b-form-input>
            <b-form-input required class='mt-2' type="email" placeholder="Укажите email для связи с Вами"></b-form-input>
            <button class='send-btn' style='height: 50px; width: 100%; margin-top: 10px;'>Отправить</button>
        </div>
      </div>

    </div>
  </section>
</template>

<script>
export default {
  name: 'photoset',

  data() {
    return {
      services: {}
    }
  },

  props: {
  },

  async created() {
    await this.getPhotosetsDescriptions()
    console.log(this.services);
  },

  methods: {
    openSidebar(photosetType) {
      for (let ref in this.$refs) {
        if (this.$refs[ref][0]) {
          let refItemStyle = this.$refs[ref][0].style;
          console.log(refItemStyle);
          refItemStyle.opacity='0';
          refItemStyle.pointerEvents = 'none'
        }
        // if (refItemStyle.opacity == '1') {
        // }
      }
      this.$refs.titlesPart.style.width = '50%';
      this.$refs[`${photosetType}`][0].style.opacity = '1';
      this.$refs[`content-${photosetType}`][0].style.opacity = '1';
      this.$refs[`content-${photosetType}`][0].style.pointerEvents = 'all';
    },
    closeSidebar(photosetType) {
      this.$refs.titlesPart.style.width = '100%';
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
  .course-sect {
    background-color: white !important;
    height: 100vh;
  }

  .photosets-container {
    position: relative;
    display: flex;
    flex-direction: row;
    width: 90%;
    margin-left: 5%;
    top: 10vh;
    height: 80vh;
    background-size: cover;
    /* background-image: url('/images/background2.jpg') */
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
    width: 42vh;
    font-size: 1.1rem;
    letter-spacing: 3px;
    background: none;
    /* padding: 10px; */
    border: none;
    outline: none;
    color: white;
    font-weight: bold;
    text-transform: uppercase;
    transition: 0.2s
  }

  .photoset-btn:focus {
    outline: none;
    transform: scale(1.1, 1.1);
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
  .sidebar-content {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: justify;
    width: 80%;
    font-weight: bold;
    opacity: 0;
  }

  .sidebar-content span {
    margin-bottom: 20px;
    font-size: 20px;
  }

  .price-span {
    color: #777;
    font-size: 25px
  }

  .send-btn {
    background: none;
    border: none;
    outline: none;
    color: white;
    font-weight: bold;
    text-transform: uppercase;
    transition: 0.2s
  }

  .send-btn:hover {
    transform: scale(1.1, 1.1);
  }

  .close-sidebar-btn {
    cursor: pointer;
  }
</style>

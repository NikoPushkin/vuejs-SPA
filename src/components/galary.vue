<template>
    <swiper class="swiper" :options="swiperOption">
      <swiper-slide v-for='image in photoSetSources' :key='image.id'>
        <!-- <div> -->
          <img ref='sliderImage' :src="image">
        <!-- </div> -->
      </swiper-slide>
      <!-- <div class="swiper-pagination" slot="pagination"></div>
      <div class="swiper-button-prev" slot="button-prev"></div>
      <div class="swiper-button-next" slot="button-next"></div> -->
    </swiper>


</template>

<script>
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'

import 'swiper/swiper-bundle.css'

export default {
  name: 'GalaryComponent',
  components: {
    Swiper,
    SwiperSlide
  },
  data() {
    return {
      index: null,
      photoSetSources: [
          "/images/photo1.jpg",
          "/images/photo7.jpg",
          "/images/photo5.jpg",
          "/images/photo6.jpg",
          "/images/photo3.jpg",
          "/images/photo8.jpg",
          ],
      swiperOption: {
        slidesPerView: 3,
        slidesPerGroup: 3,
        spaceBetween: 30,
        pagination: {
          el: '.swiper-pagination',
          clickable: true
        },
        breakpoints: {
          1024: {
            slidesPerView: 3,
            spaceBetween: 40,
          },
          768: {
            slidesPerView: 2,
            spaceBetween: 30,
            slidesPerGroup: 2,
          },
          0: {
            slidesPerView: 1,
            slidesPerGroup: 1,
            spaceBetween: 20,
          },

        }
      },
    }
  },
}
</script>
<style  scoped>

.swiper {
  height: 70%;
  width: 90%;
}

.swiper-slide {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.swiper-slide img {
  width: 100%;
  padding: 0px 20px;
  /* height: 800px; */
  object-fit: cover !important;
  transition: 0.4s;
}

/* @media only screen and (max-width: 1640px) {
  .swiper-slide img {
    width: 500px;
    height: 500px;
    object-fit: cover !important;
    transition: 0.4s;
  }
}

@media only screen and (max-width: 1400px) {
  .swiper-slide img {
    width: 350px;
    height: 500px;
    object-fit: cover !important;
    transition: 0.4s;
  }
}

@media only screen and (max-width: 768px) {
  .swiper-slide img {
    width: 100%;
    max-width: 600px;
    height: 400px;
    object-fit: cover !important;
    transition: 0.4s;
  }
} */

</style>

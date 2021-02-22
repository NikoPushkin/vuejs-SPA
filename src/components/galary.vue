<template>
    <swiper ref='mySwiperRef' class="swiper" :options="swiperOption">
      <swiper-slide v-for='image in photoSetSources' :key='image.id'>
        <!-- <div> -->
          <img ref='sliderImage' :src="image">
        <!-- </div> -->
      </swiper-slide>
      <div class="swiper-button-prev" @click='prev' slot="button-prev"></div>
      <div class="swiper-button-next" @click='next' slot="button-next"></div>
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
        loop: true,
        breakpoints: {
          1600: {
            slidesPerView: 3,
            spaceBetween: 40,
          },
          1280: {
            slidesPerView: 2,
            spaceBetween: 30,
            slidesPerGroup: 2,
          },
          0: {
            slidesPerView: 1,
            slidesPerGroup: 1,
            spaceBetween: 20,
          },
        },
      },
    }
  },
  methods: {
    next() {
      this.$refs.mySwiperRef.$swiper.slideNext()
    },
    prev() {
      this.$refs.mySwiperRef.$swiper.slidePrev()
    },
  },
}
</script>
<style  scoped>

.swiper {
  height: 100%;
  width: 90%;
  background-color: beige
}

.swiper-slide {
  display: flex;
  margin-top: 5vh;
  justify-content: center;
  clip-path: inset(0 0 0 0);
}

.swiper-slide img {
  height: 90%;
  object-fit: cover !important;
  transition: 0.4s;
}
</style>

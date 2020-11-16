<template>
    <swiper class="swiper" :options="swiperOption">
      <swiper-slide v-for='image in photoSetSources' :key='image.id'>
        <div>
          <img :src="image" alt="">
        </div>
      </swiper-slide>
      <!-- <swiper-slide>Slide 2</swiper-slide>
      <swiper-slide>Slide 3</swiper-slide>
      <swiper-slide>Slide 4</swiper-slide>
      <swiper-slide>Slide 5</swiper-slide>
      <swiper-slide>Slide 6</swiper-slide>
      <swiper-slide>Slide 7</swiper-slide> -->
      <div class="swiper-pagination" slot="pagination"></div>
      <!-- <div class="swiper-button-prev" slot="button-prev"></div>
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
          "/images/photo7.jpg",
          "/images/photo1.jpg",
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
        }
      }
    }
  },
}
</script>
<style  scoped>
.swiper {
  height: 80vh;
  width: 95%;
  margin-top: 4%
}

.swiper-slide {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  /* font-weight: bold;
  font-size: 10 * 2; */
  /* background-color: black; */
}
.swiper-slide img {
  width: 100%;
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
}

</style>

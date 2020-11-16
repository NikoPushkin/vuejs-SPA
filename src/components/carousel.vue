<template>
  <carousel :data="data"></carousel>
</template>

<script>
export default {
  name: 'VueCarousel',
  props: {
  },
  data: function() {
return [
  '<div class="carousel-slide">Slide 2</div>',
  '<div class="carousel-slide">Slide 3</div>',
  '<div class="carousel-slide">Slide 1</div>',
  ];
},
}
</script>

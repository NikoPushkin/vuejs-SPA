<template>
  <section id='ГАЛЕРЕЯ' class='galary-sect'>
    <div class="photo-row">
      <div class="column" :key='col.id' v-for='(col, index) in photoSetSources'>
        <img :src='source' :key='source.id' v-for='source in photoSetSources[index]'>
      </div>
    </div>
  </section>
</template>

<script>

export default {
  name: 'GalaryComponent',
  components: {
  },
  props: {
  },

  data() {
    return {
      slide: 0,
      sliding: null,
      photoSetSources: [
                          [ "/images/photo6.jpg",
                          "/images/photo1.jpg",
                          "/images/photo5.jpg" ],
                         [ "/images/photo4.jpg",
                           "/images/photo7.jpg",
                           "/images/photo3.jpg" ],
                         [ "/images/photo9.jpg",
                           "/images/photo8.jpg",
                           "/images/photo2.jpg" ] ],
    }
  },

  mounted() {
  },

  methods: {
    onSlideStart() {
      this.sliding = true
    },
    onSlideEnd() {
      this.sliding = false
    }
  }
}
</script>
<style>

img {
  pointer-events: none;
}

.photo-row {
display: flex;
flex-wrap: wrap;
padding: 0 4px;
}

/* Create four equal columns that sits next to each other */
.column {
flex: 33.3%;
max-width: 33.3%;
padding: 0 4px 10px;
}

.column img {
margin-top: 8px;
vertical-align: middle;
width: 100%;
height: auto;
}

/* Responsive layout - makes a two column-layout instead of four columns */
/* @media screen and (max-width: 800px) {
.column {
  flex: 50%;
  max-width: 50%;
}
} */

/* Responsive layout - makes the two columns stack on top of each other instead of next to each other */
@media screen and (max-width: 600px) {
.column {
  flex: 100%;
  max-width: 100%;
}
}
</style>

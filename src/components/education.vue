<template>
  <section id='ОБУЧЕНИЕ' class='course-sect'>
    <div class="photosets-container">
      <div class="photoset-titles">
        <p>dasd</p>
        <p>dasd</p>
        <p>dasd</p>
        <b-button @click='openSidebar()'>Toggle Sidebar</b-button>

      </div>

      <div ref='photosetSidebar' class="photoset-description" id='photoset-sidebar'>
        <div class="sidebar-content">
          <p>dasd</p>
          <p>dasd</p>
          <b-button @click='closeSidebar()'>cl</b-button>
        </div>

      </div>

    </div>
  </section>
</template>

<script>
export default {
  name: 'EducationComponent',
  props: {
  },
  methods: {
    openSidebar() {
      console.log(this.$refs);
      this.$refs.photosetSidebar.style.width='50%'
      this.$refs.photosetSidebar.children[0].style.visibility = 'visible'
    },
    closeSidebar() {
      this.$refs.photosetSidebar.style.width='0px'
      this.$refs.photosetSidebar.children[0].style.visibility = 'hidden'

    }
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
    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), url('/images/background2.jpg');
  }

  .photoset-titles {
    display: flex;
    flex-direction: column;
    width: 50%;
    heigth: 100%;
    justify-content: space-around;
    align-items: center;
  }

  .photoset-description {
    position: absolute;
    width: 0%;
    height: 100%;
    background-color: transition;
    transition: 0.4s;
    transform: translateX(0);
    right: 0 !important;
    left: auto;
  }
  .sidebar-content {
    visibility: hidden;
    transition: 0.3s
  }
</style>

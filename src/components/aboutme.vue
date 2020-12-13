<template>
  <!-- <div> -->
    <!-- <b-modal id="modal-scrollable" centered button-size='400' hide-header ok-only ok-variant='light' ok-title='ЗАКРЫТЬ'> -->
      <div class="card-container">
          <div class="card-wrapper">
            <div class="card-left">
              <div class="card-left-text">
                <h1>Вероника Вегера</h1>
                <p class='job-title'>Фотограф</p>
                <p class='about'>
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit,
                  sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
                  Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris
                  nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit
                  in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
                  Excepteur sint occaecat cupidatat non proident, sunt in culpa qui
                  officia deserunt mollit anim id est laborum.
                </p>
              </div>
            </div>
            <div class="card-right">
              <img src="/images/avatar.jpg" alt="profiile-img" class='profile-img'>
              <img src="/images/background.jpg" alt="card background" class='card-img'>
            </div>
          </div>
      </div>
    <!-- </b-modal> -->
  <!-- </div> -->
</template>

<script>
export default {
  name: 'AboutMeComponent',
  props: {
  },
  data() {
    return {
    }
  }
}
</script>

<style media="screen">

.card-container {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  top: 10vh;
  height: 80%;
  width: 100%
}

.card-wrapper {
  position: relative;
  height: 100%;
  width: 90%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-left {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 50%;
  height: 100%;
  align-items: flex-start;
  background-color: #e3e0e040
}

.card-left-text {
  display: flex;
  flex-direction: column;
  width: 80%;
  align-items: center;
}

.card-right {
  width: 50%;
  height: 100%;
  background-color: white;
  display: flex;
  border: none !important;
}

.card-right .card-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  clip-path: inset(0 0 0 0);
}

.profile-img {
  position: absolute;
  width: 18rem;
  height: 18rem;
  margin-left: -9rem;
  margin-top: 25vh;
  object-fit: cover;
  border-radius: 50%;
  z-index: 1;
  border: 0.2rem solid white

}

.card-left-text h1 {
  color: #333;
}

.job-title {
  color: #777;
  font-size: 1.4rem;
  font-weight: 300;
  margin-bottom: 1.4rem;
}

.about {
  width: 80%;
  font-size: 1.2rem;
  font-style: italic;
  text-align: center;
  color: #333;
}

.swiper-button-next, .swiper-button-prev {
  color: white !important;
  padding: 5px !important;
  border-radius: 50%;
  width: calc(var(--swiper-navigation-size) / 18 * 27) !important;
  height: calc(var(--swiper-navigation-size)*1.5) !important;
  transition: 0.4s;
}

.swiper-button-next:hover, .swiper-button-prev:hover {
  background-color: #e3e0e040;
  transform: scale(1.1, 1.1);
}

@media screen and (max-width: 300px){
  .card-wrapper {
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
  }

  .modal-body{
    border: none
  }

  .card-right {
    border: none !important;

  }

  .card-right .card-img {
    height: 12rem;
  }

  .card-right h1 {
    font-size: 1.5rem;
    margin: 0.5rem 0
  }

  .about {
    font-size: 0.8rem;
    margin: 2px
  }
}
</style>

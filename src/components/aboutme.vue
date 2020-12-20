<template>
  <!-- <div> -->
    <!-- <b-modal id="modal-scrollable" centered button-size='400' hide-header ok-only ok-variant='light' ok-title='ЗАКРЫТЬ'> -->
    <div class="aboutme-container">
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
      <div class="mobile-card-container">
        <div class="mobile-card-wrapper">
          <img src="/images/avatar.jpg" alt="profile-img" class='mobile-profile-img'>
          <div class="sidebar-btn">
            <p class="main-about-text">
              <span>Veronika Vegera</span>
              <span>Photography</span>
            </p>
            <button v-b-toggle.mainpage-sidebar>ОБО МНЕ</button>
          </div>
          <b-sidebar id="mainpage-sidebar" title="Приветствую тебя на моем сайте!" cshadow>
            <div class="px-3 py-2">
              <p>
                Cras mattis consectetur purus sit amet fermentum. Cras justo odio, dapibus ac facilisis
                in, egestas eget quam. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.
              </p>
            </div>
          </b-sidebar>
        </div>
      </div>
    </div>
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

/*

* DESKTOP ABOUTME PAGE STYLES

 */


.aboutme-container {
  width: 100%;
  height: 100%;
}
.mobile-card-container {
  display: none;
}

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

/*

* DESKTOP ABOUTME PAGE STYLES
********************************************************************************
 */


/*

* MOBILE ABOUTME PAGE STYLES

 */

@media screen and (max-width: 1200px){
  .profile-img {
    width: 12rem;
    height: 12rem;
    margin-left: -6rem;
    margin-top: 28vh;
  }

  .card-left h1 {
    font-size: 1.5rem;
    margin: 0.5rem 0
  }

  .about {
    font-size: 0.8rem;
    margin: 2px
  }
}


@media screen and (max-width: 800px){
  .card-container {
    display: none;
  }

  .mobile-card-container {
    position: absolute;
    display: block;
    height: 80vh;
    width: 100%;
    margin-top: 10vh
  }

  .mobile-card-wrapper {
    display: flex;
    align-items: center;
    align-content: center;
    flex-direction: column;
  }

  .card {
    width: 100%;
    height: 100%;
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .mobile-profile-img {
    clip-path: inset(0 0 0 0);
    width: 90%;
    height: 80vh;
    object-fit: cover;
    z-index: 1;
  }

  #mainpage-sidebar {
    height: 80vh !important;
    top: 10vh !important;
    width: 100% !important;
    text-align:justify !important;
    word-break:keep-all !important;
  }

  .b-sidebar-header {
    /* text-align: center !important; */
  }

  .sidebar-btn {
    position: absolute;
    display: flex;
    flex-direction: column;
    width: 90%;
    height: 80vh;
    align-items: center;
    justify-content: center;
    z-index: 2;
    background: rgb(0, 0, 0);
    background: rgba(0, 0, 0, 0.5);
    color: #f1f1f1;
    text-align: center;
    padding-top: 7em
  }

  .sidebar-btn button {
    padding: 0px 35px;
    background-color: white;
    background: rgba(0, 0, 0, 0.5);
    border: none;
    outline: none;
    color: white;
    font-size: 1.6em;
    letter-spacing: 8px
  }

  .main-about-text span {
    display: block;
  }

  .main-about-text span:first-of-type {
    margin-bottom: -10px;
    letter-spacing: 7px;
    font-size: 1.2em;
  }

  .main-about-text span:last-of-type {
    margin-bottom: -10px;
    letter-spacing: 8px;
    font-weight: bold;
    font-size: 1.6em;
  }
}
</style>

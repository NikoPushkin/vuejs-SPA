<template>
  <div>
    <b-modal id="modal-scrollable" centered button-size='400' hide-header ok-only ok-variant='light' ok-title='ЗАКРЫТЬ'>
      <div class="card-container">
        <h1 class="heading"></h1>
          <div class="card-wrapper">
            <div class="card">
              <img src="/images/background.jpg" alt="card background" class='card-img'>
              <img src="/images/avatar.jpg" alt="profiile-img" class='profile-img'>
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
      </div>
    </b-modal>
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

.modal-body {
  /* padding: 0 !important */
  pointer-events: all !important;
}

.modal-content {
  border-radius: 0 !important;
  z-index: 100
}

.modal-footer {
  justify-content: center !important;
  padding: 1px !important;
}
.modal-footer .btn {
  border-radius: 0 !important;
  background-color: white;
  color: black;
  letter-spacing: 0.5px;
  width: 50%;
  border: none;
}

.modal-footer .btn:hover {
  background-color: black;
  color: white
}

.card-wrapper {
  display: flex;
  align-items: center;
  align-content: center;
  flex-direction: column;
}

.card {
  width: 100%;
  background-color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0rem 0;
}

.card .card-img {
  width: 100%;
  height: 15rem;
  object-fit: cover;
  clip-path: inset(0 0 0 0);
}

.profile-img {
  width: 10rem;
  height: 10rem;
  object-fit: cover;
  border-radius: 50%;
  margin-top: -5rem;
  z-index: 1;
  border: 0.2rem solid white

}

.card h1 {
  font-size: 2rem;
  color: #333;
  margin: 1rem 0;
}

.job-title {
  color: #777;
  font-size: 1.2rem;
  font-weight: 300;
  margin-bottom: 1rem
}

.about {
  margin-top: 0;
  font-size: 1rem;
  font-style: italic;
  text-align: center;
  color: #333;
  padding: 0 5px;
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

  .card {
    border: none !important;

  }

  .card .card-img {
    height: 12rem;
  }

  .card h1 {
    font-size: 1.5rem;
    margin: 0.5rem 0
  }

  .about {
    font-size: 0.8rem;
    margin: 2px
  }
}
</style>

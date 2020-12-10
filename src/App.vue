<template>
  <div id="app">
    <AboutMeComponent></AboutMeComponent>
    <div class='full-navbar-container'>
      <ul class='full-navbar'>
        <li
          class='navbar-button'
          :data-menuanchor="Object.values(elem)[0]"
          v-for='elem in navbarElems'
          :key="elem.id"
          ref='navbarButtons'
          >
            <a v-if='Object.keys(elem)[0]=="ОБО МНЕ"'
                v-b-modal.modal-scrollable
                :href="'#'+Object.values(elem)[0]"
            >
              {{ Object.keys(elem)[0] }}
            </a>
            <a :href="'#'+Object.values(elem)[0]"
                v-else>
              {{ Object.keys(elem)[0] }}
            </a>
        </li>
      </ul>
    </div>


    <full-page :options="options" id="fullpage">
      <div class="section">
        <GalaryComponent></GalaryComponent>
      </div>
      <div class="section">
        <Photoset :csrfToken='csrfToken'></Photoset>
      </div>

      <div class="section">
        <EducationComponent></EducationComponent>
      </div>


      <div class="section">
          <div id="mySidenav" class="sidenav">
            <table class="sidenav-table">
              <tr><a href="javascript:void(0)" class="closebtn" @click="closeNav()">&times;</a></tr>
              <tr><a href="https://www.instagram.com/vegeraveronika"><i class="fab fa-instagram"></i></a></tr>
              <tr><a href="https://vk.com/vegeraveronika"><i class="fab fa-vk"></i></a></tr>
              <tr><a href="https://t.me/lumosphoto"><i class="fab fa-telegram"></i></a></tr>
            </table>
          </div>
      </div>
    </full-page>
    <div class='mainPageFooter'>
      <h4>Veronika Vegera Photography</h4>
      <!-- <div class="">
        <a href="https://www.instagram.com/vegeraveronika"><i class="fab fa-instagram"></i></a>
        <a href="https://vk.com/vegeraveronika"><i class="fab fa-vk"></i></a>
        <a href="https://t.me/lumosphoto"><i class="fab fa-telegram"></i></a>
      </div> -->
    </div>
  </div>
</template>

<script>
import Photoset from './components/photoset.vue'
import AboutMeComponent from './components/aboutme.vue'
import EducationComponent from './components/education.vue'
import GalaryComponent from './components/galary.vue'

export default {
  name: 'App',
  components: {
    Photoset,
    GalaryComponent,
    EducationComponent,
    AboutMeComponent,
  },
  data () {
    return {
      options: {
        licenseKey: 'YOUR_KEY_HERE',
        afterLoad: this.afterLoad,
        scrollOverflow: true,
        scrollBar: false,
        menu: '#menu',
        navigation: true,
        anchors: ['/about', '/photoset', '/education'],
        sectionsColor: ['#FFFFFF  ', '#FFFFFF', '#FFFFFF', '#FFFFFF', '#1bcee6', '#ee1a59', '#2c3e4f', '#ba5be9', '#b4b8ab']
      },
      navbarElems: [
        { 'ОБО МНЕ': '/about' },
        // { 'ГАЛЕРЕЯ': '/galary' },
        { 'ОБУЧЕНИЕ': '/education' },
        { 'CЪЕМКА': '/photoset' },
        { 'КОНТАКТЫ': 'null'}
      ],

      contactsList: [
        'https://www.instagram.com/vegeraveronika',
        'https://vk.com/vegeraveronika',
        'https://t.me/lumosphoto'
      ],

      contactsIndicator: true,
      csrfToken: ''
      }
    },
    created() {
      this.csrfToken = this.getCookie('csrftoken');
      console.log(this.csrfToken);
    },
    watch: {
    },
    methods: {
      scroll(elem) {
        console.log(elem);
        let element = document.getElementById(elem);
        document.getElementById("mySidenav").style.width = "0";
        this.contactsIndicator = true
        element.scrollIntoView({ behavior: 'smooth' });
      },
      openNav() {
        if (this.contactsIndicator) {
          document.getElementById("mySidenav").style.width = "15%";
          this.contactsIndicator = !this.contactsIndicator
        } else {
          document.getElementById("mySidenav").style.width = "0";
          this.contactsIndicator = true
        }
      },

      /* Set the width of the side navigation to 0 */
      closeNav() {
        document.getElementById("mySidenav").style.width = "0";
        this.contactsIndicator = true
      },

      // get csrf-token for making POST-request to Django
      getCookie(name) {
        let cookieValue = null;
        if (document.cookie && document.cookie !== '') {
            const cookies = document.cookie.split(';');
            for (let i = 0; i < cookies.length; i++) {
                const cookie = cookies[i].trim();
                // Does this cookie string begin with the name we want?
                if (cookie.substring(0, name.length + 1) === (name + '=')) {
                    cookieValue = decodeURIComponent(cookie.substring(name.length + 1));
                    break;
                }
            }
        }
        return cookieValue;
      }
  },


}
</script>

<style src="@/assets/styles/mainPage.css">
</style>

<template>
  <section id='CЪЕМКА'>
    <div class='photoset-cont' ref='photocont'>
      <div class="button-bar" :ref='"button-"+index' :key='service.id' v-for='(service, index) in services'>
        <button :class='"button-"+index' @click='collapseVisibilityControl("collapse-", index)'
                >
          {{ Object.values(service)[0] }}
        </button>
        <b-collapse :class='"collapse-"+index' v-model='collapseVisibility["collapse-"+index]'
                    style='color: black;' class="mt-2"
                    >
          <b-card style="max-width: 22rem;" class='pl-0'>
            <p class='about'>
              {{ Object.values(service)[1] }}

            </p>
            <div class='job-title'
              >
              {{ Object.values(service)[2] }}&#8381;
              <div class='book-service'
                @click='collapseVisibilityControl("subCollapse-", index)'
                >
                <i class="fas fa-feather-alt book-icon"></i>
              </div>
            </div>
            <b-collapse v-model='collapseVisibility["subCollapse-"+index]' class="mt-2">
              <b-form-input required type="text" placeholder="Как Вас зовут?"></b-form-input>
              <b-form-input required class='mt-2' type="email" placeholder="Укажите email для связи с Вами"></b-form-input>
              <button style='height: 50px; width: 100%; margin-top: 10px;'>Отправить</button>
            </b-collapse>
          </b-card>
        </b-collapse>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'PhotoSet',
  props: {
    csrfToken: String
  },
  data() {
    return {
      services: {},
      collapseVisibility: {
                  'collapse-0': false,
                  'collapse-1': false,
                  'collapse-2': false,
                  'subCollapse-0': false,
                  'subCollapse-1': false,
                  'subCollapse-2': false,
                },
      emailForm: {
        message_name: 'ololololo',
        message_email: 'nikopushkin1@gmail.com',
        message: 'hehehehehehe'
      }
    }
  },

  created() {
    // this.sendEmail(this.csrfToken)
    this.getPhotosetsDescriptions()
  },

  methods: {
    collapseVisibilityControl(collapse, id) {
      // closes collapse and moves button to the section center
      if (this.collapseVisibility[`${collapse}${id}`]) {
        this.collapseVisibility[`${collapse}${id}`] = !this.collapseVisibility[`${collapse}${id}`]
        if (collapse != 'subCollapse-') {
          this.$refs[`button-${id}`][0].style.marginTop = '20%'
        }
      // открывает коллапс и смещает кнопку к потолку
      } else {
        // let stay opened only one collapse at the moment
        if (this.$refs['photocont'].clientWidth < 1200 && collapse != 'subCollapse-') {
          for (let i in this.collapseVisibility) {
            this.collapseVisibility[i] = false
          }
          this.collapseVisibility[`${collapse}${id}`] = !this.collapseVisibility[`${collapse}${id}`]
          // it is possible to open multiple collapses
        } else {
          this.collapseVisibility[`${collapse}${id}`] = !this.collapseVisibility[`${collapse}${id}`]
          this.$refs[`button-${id}`][0].style.marginTop = '4%'
        }
      }

    },
    // get services descriptions
    async getPhotosetsDescriptions() {
      let response = await fetch('http://127.0.0.1:8000/api/get-descriptions');
      if (response.ok) {
        let json = await response.json();
        this.services = json
      } else {
        console.log('Error' + response.status);
        return;
      }
    },

    async sendEmail(token) {
      const request = new Request(
              'http://127.0.0.1:8000/api/send-email',
              {headers: {'X-CSRFToken': token}}
            )
      let data = this.emailForm
      let response = await fetch(request, {
                                  method: 'POST',
                                  body: JSON.stringify(data),
                                  credentials: 'include'
                                })
      return response
    },
  }
}
</script>

<style media="screen">
.job-title {
  text-align: center;
  color: #777;
  font-size: 1.2rem;
  font-weight: 300;
  margin-bottom: 1rem
}

.about {
  margin-top: 0;
  font-size: 1rem;
  text-align: justify;
  color: #333;
}

.photoset-cont {
  /* background-color: white; */
  height: 100vh;
  display: flex;
  justify-content: center;
}

.button-bar {
  margin-top: 20%;
  transition: .4s

}

.button-bar button {
  background-color: black;
  letter-spacing: 1px;
  position: sticky;
  clip-path: polygon(40 0 0 0);
  width: 22rem;
  height: 10rem;
  color: white;
  font-size: 1.3rem;
  outline: none;
  border: none;
  transition: .4s
}

.book-service {
  display: inline-block;
  color: blue;
  padding: 0px 10px;
  transition: .4s;
  outline: none
}

.book-service:hover {
  transform: scale(1.4, 1.4);
  cursor: pointer;
}

input[type="button"]::-moz-focus-inner {
   border: 0;
}

button:focus {
  outline: none !important;
}

.button-1, .collapse-1 {
  margin-right: 5vh;
  margin-left: 5vh
}

.button-bar button:hover {
  transform: scale(1.1, 1.1);
}

@media screen and (max-width: 1200px){
  .photoset-cont {
    align-items: center;
    flex-direction: column;
    justify-content: flex-start;
  }

  .button-1, .collapse-1 {
    margin-right: 0px;
    margin-left: 0px
  }

  .button-bar {
    margin-top: 2% !important;
    text-align: center;
  }

  .button-bar button:hover {
    transform: scale(1.02, 1.02);
  }
}

/* iphone 5 screen */
@media screen and (max-width: 320px){
  .button-bar button {
    width: 19rem;
  }
}
/* galaxy fold screen */
@media screen and (max-width: 280px){
  .button-bar button {
    width: 17rem;
  }
}



</style>

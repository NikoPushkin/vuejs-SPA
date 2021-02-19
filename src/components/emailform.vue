<template>
  <div class="email-form-container">
    <b-modal hide-footer hide-header centered cshadow id="email-form-modal" title="">
      <div  class="d-block text-right ">
        <div @click="closeModal()" style='cursor: pointer' class="d-inline">
          <i class="fas fa-times"></i>
        </div>
      </div>
      <!-- <h2 class='text-center' style='color: white'>Форма обратной связи</h2> -->
      <div style='height:3px; background-color: black; margin-top: 0.2rem'></div>
        <div class="" style='display: flex; justify-content: space-evenly; padding: 0.3rem;'>
          <div style='color: black; letter-spacing: 1px; font-size: 2vh' class="">{{ type }}</div>
          <div style='color: black; letter-spacing: 1px; font-size: 2vh' class="">{{ price }}&#8381;</div>
        </div>
      <div class='mb-4' style='height:3px; background-color: black'></div>
      <!-- <div style='color: black; letter-spacing: 1px' class="price-span text-center">{{ type }}</div>
      <div style='color: black; letter-spacing: 1px' class="mt-2 mb-5 price-span text-center">{{ price }} &#8381;</div> -->
      <b-form-input required type="text" placeholder="Как Вас зовут?"></b-form-input>
      <b-form-input required class='mt-2' type="email" placeholder="Укажите email для связи с Вами"></b-form-input>
      <button class='send-btn btn-class hover-transform-btn' style='height: 50px; width: 100%; margin-top: 10px; color: black'>Отправить заявку</button>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: 'emailFormComponent',
  props: {
    type: {
      required: true,
      default: null
    },
    price: {
      required: true,
      default: '  '
    }
  },
  data() {
    return {
    }
  },
  methods: {
    closeModal() {
      this.$root.$emit('bv::hide::modal', 'email-form-modal')
    },
    async sendEmail(token) {
      console.log('TOKEN: ', token);
      var request = new Request(
              'http://127.0.0.1:8000/api/send-email',
              {headers: {'X-CSRFToken': token }}
            );
      let data = this.emailForm;
      let response = await fetch(request, {
                                  method: 'POST',
                                  body: JSON.stringify(data),
                                  credentials: 'include'
                                });
      return response;
    },
  },
}
</script>

<style media="screen">
#email-form-modal div {
  border: none !important;
}

#email-form-modal .modal-content {
  background: #fffffff5 !important;
  /* background: #000000eb !important; */
}
#email-form-modal .modal-body {
  padding-top: 0.5rem
}

#email-form-modal button {
  color: black;
  outline: none
}
</style>

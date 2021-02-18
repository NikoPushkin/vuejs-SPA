<template>
  <div class="email-form-container">
    <b-modal hide-footer centered cshadow id="email-form-modal" title="">
      <!-- <h2 class='text-center' style='color: white'>Форма обратной связи</h2> -->
      <div style='color: white' class="price-span text-center">{{ type }}</div>
      <div style='color: white' class="mt-2 mb-5 price-span text-center">{{ price }}&#8381;</div>
      <b-form-input required type="text" placeholder="Как Вас зовут?"></b-form-input>
      <b-form-input required class='mt-2' type="email" placeholder="Укажите email для связи с Вами"></b-form-input>
      <button class='send-btn btn-class hover-transform-btn' style='height: 50px; width: 100%; margin-top: 10px;'>Отправить заявку</button>
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
}
}
</script>

<style media="screen">
#email-form-modal div {
  border: none !important;
}

#email-form-modal .modal-content {
  background: #000000eb !important;
}

#email-form-modal header {
  border: none !important;
  padding-top: 1rem ;
  padding-right: 1rem ;
  padding-bottom: 0 ;
  padding-left: 1rem
}

#email-form-modal button {
  color: white;
  outline: none
}
</style>

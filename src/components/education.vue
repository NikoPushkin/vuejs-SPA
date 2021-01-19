<template>
    <div class="education-container">
      <div ref='leftPart' class="education-left-part">
        <div class="left-part-content">
          <p>индивидуальное обучение</p>
          <div class="days-btns-container">
            <button  class='btn-class' @click='openDescription(day.number)' :key='day.id' v-for='day in educationDays'>{{ day.number }}</button>
          </div>
        </div>
      </div>

      <div :ref='day.number' class="education-right-part" :key='day.id' v-for='day in educationDays'>
        <div :ref='"description-"+day.number' class="day-description">
          <div class="close-btn-box">
            <span class='close-btn hover-transform-btn' @click='closeDescription(day.number)'><i class="fas fa-times"></i></span>
          </div>

          <span ref='daysContent' class="days-content"> {{ day.description }}</span>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'EducationComponent',

  data() {
    return {
      educationDays: {
        // 1: {number: 'УСЛОВИЯ', description: '- Обучение проходит в формате online-лекции, через SKYPE.<br>- Продолжительность одной лекции: 2 - 2.5 часа <br>- Стоимость обучения - 7500 рублей.<br>*Для бронирования даты необходимо внести задаток в размере - 2500 рублей.'},
        1: {number: 'УСЛОВИЯ', description: 'dsadsad'},
        2: {number: 'День I', description: '- Портрет, понятие его жанров.<br>- Свет. Основы. Разбор естественного света. Световая иерархия, как работать с любым источником света?<br>- Референс как путь к собственному стилю, как грамотно составлять мудборд, вдохновение без задержек. Творческая дисциплина.'},
        3: {number: 'День II', description: '- Грамотное планирование съемки, подробный разбор нюансов подготовки к процессу.<br>- Методы поиска локаций, моделей, одежды.<br>- Модель, кто это? Основные понятия, особенности работы с профессиональными и непрофессиональными моделями. Какие ошибки вы можете допустить при работе в обеих случаях. Рабочая этика.<br>- Проблемы и конфликтные ситуации, как избежать. Влияние на психологическое состояние модели. Особенности сотрудничества с Визажистом/стилистом.<br>- Работа с моделью на съемке, установление психологического контакта Фотограф- модель. Как добиться эмоций, чувственности. Завершение съемки, почему важно получить обратную связь.'},
        4: {number: 'День III', description: '- Работа с цветом. Основные понятия, цветовые гармонии, композиция цвета.Обработка. <br>- Lightroom: Инструменты для цветокоррекции снимков, применение. Тоновая кривая, принципы работы. Основные приемы колористики, как применять их в фотографии. Экспорт фотографий. Свободные вопросы. <br>- Photoshop: Ретушь «Без ретуши» деликатный способ устранения нюансов с естественным эффектом. Коррекция формы, работа с инструментом «пластика», как и где применяю. Устранение лишних деталей с кадра, резкость, объем и блики. <br>- Портфолио Ревю. Рекомендации и свободные вопросы.'},
      }
    }
  },

  props: {
  },

  async created() {

  },

  methods: {
    closeOpenedDescription() {
      for (let ref in this.$refs) {
        if (this.$refs[ref][0]) {
          let refItemStyle = this.$refs[ref][0].style;
          refItemStyle.opacity='0';
          refItemStyle.pointerEvents = 'none'
        }
      }
    },

    openDescription(descriptionRef) {
      this.closeOpenedDescription();
      // move photoset-titles to the left side when description window is opened
      this.$refs.leftPart.style.width = '50%';

      // opens fullscreen description if screen size is small
      if (window.screen.width < 950) {
        this.$refs.leftPart.style.display = 'none';
      }
      // show description window
      this.$refs[`${descriptionRef}`][0].style.opacity = '1';
      this.$refs[`description-${descriptionRef}`][0].style.opacity = '1';
      this.$refs[`description-${descriptionRef}`][0].style.pointerEvents = 'all';
    },

    closeDescription(descriptionRef) {
      // move photoset-titles to the center side when description window is opened
      this.$refs.leftPart.style.width = '100%';

      if (window.screen.width < 950) {
        this.$refs.leftPart.style.display = 'flex'
      }
      // hide description window
      this.$refs[`${descriptionRef}`][0].style.opacity = '0'
      this.$refs[`description-${descriptionRef}`][0].style.opacity = '0';
      this.$refs[`description-${descriptionRef}`][0].style.pointerEvents = 'none';
    }
  }
}
</script>

<style media="screen">
.education-container {
  position: relative;
  display: flex;
  flex-direction: row;
  background-size: cover;
  background-image: url('/images/edbg2.jpg');
  width: 90%;
  margin-left: 5%;
  top: 5vh;
  height: 90vh;
}

.education-left-part {
  font-family: 'Courier New', monospace;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;
  text-align: center;
  transition: 0.2s
}


.education-left-part p {
  /* font-weight: bold; */
  font-size: 3vh;
  letter-spacing: 5px;
  text-transform: uppercase;
}

.left-part-content {
  display: block;
}

.days-btns-container {
  /* position: relative; */
  width: 100%;
  display: grid;
  grid-template-columns: 50% 50%;
  justify-content: center;
  grid-gap: 1.6vh;
  justify-items: center;
  align-items: center;

}

.days-btns-container button {
  border: 1px solid;
  color: black;
  width: 100%;
  padding: 10px 0;
  font-size: 2.3vh;
  letter-spacing: 2px;
  /* font-weight: bold; */
}

.education-right-part {
  position: absolute;
  width: 50%;
  height: 100%;
  transition: 0.4s;
  right: 0 !important;
  left: auto;
  opacity: 0;
  background-color:white;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-content: center;
  pointer-events: none;
  color: black;
  text-align: justify;
}

@media screen and (max-width: 1100px) {
  .education-right-part {
    width: 100%
  }
  .days-btns-container button {
    font-size: 1.8vh;
    font-weight: bold;
  }
}
@media screen and (max-width: 450px) {
  .education-left-part p {
    font-size: 2.2vh;
    letter-spacing: 2px;
    text-transform: uppercase;
  }
}
</style>

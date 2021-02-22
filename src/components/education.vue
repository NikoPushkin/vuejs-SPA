<template>
    <div class="education-container">
      <div ref='leftPart' class="education-left-part">
        <img src="/images/book.jpg" alt="" class="bookImage">
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

          <div class="description-image-class">
            <img :src="day.image" alt="">
          </div>
          <div class='horizontal-line-black mb-3 mt-1' style='background-color: #000000b8; height: 2px'></div>
          <span ref='daysContent' class="days-content" style="line-height: 2.5vh; padding-bottom: 3px; margin-bottom: 3px; text-indent: 3px; width: 100%" :key='point.id' v-for="point in day.description"> <span style="font-size: 2.5vh; text-indent: 0">&#9900;</span> {{ point }}</span>
          <div class='mb-4 mt-2 horizontal-line-black' style='background-color: #000000b8; height: 2px'></div>

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
        0: {number: 'УСЛОВИЯ',
            description: {
              0: "",
              1: "Обучение проходит в формате лекции, онлайн через. Один урок длится от 2 до 2.5 часов.",
              2: "Стоимость обучения - 7500 рублей.",
              3: "Для бронирования даты необходимо внести задаток в размере - 2500 рублей."
            },
            image: "/images/book.jpg" },
        1: {number: 'День I',
            description: {
              1: "Портрет, понятие его жанров.",
              2: "Свет. Основы. Разбор естественного света. Световая иерархия, как работать с любым источником света?",
              3: "Референс как путь к собственному стилю, как грамотно составлять мудборд, вдохновение без задержек. Творческая дисциплина."
            },
            image: "/images/siluet.jpg" },
        2: {number: 'День II',
            description: {
              1: "Грамотное планирование съемки, подробный разбор нюансов подготовки к процессу.",
              2: "Методы поиска локаций, моделей, одежды.",
              3: "Модель, кто это? Основные понятия, особенности работы с профессиональными и непрофессиональными моделями. Какие ошибки вы можете допустить при работе в обеих случаях. Рабочая этика.",
              4: "Проблемы и конфликтные ситуации, как избежать. Влияние на психологическое состояние модели. Особенности сотрудничества с Визажистом/стилистом.",
              5: "Работа с моделью на съемке, установление психологического контакта Фотограф- модель. Как добиться эмоций, чувственности. Завершение съемки, почему важно получить обратную связь."
            },
            image: "/images/photo.jpg" },
        3: {number: 'День III',
            description: {
              1: "Работа с цветом. Основные понятия, цветовые гармонии, композиция цвета.Обработка.",
              2: "Lightroom: Инструменты для цветокоррекции снимков, применение. Тоновая кривая, принципы работы. Основные приемы колористики, как применять их в фотографии. Экспорт фотографий. Свободные вопросы.",
              3: "Photoshop: Ретушь «Без ретуши» деликатный способ устранения нюансов с естественным эффектом. Коррекция формы, работа с инструментом «пластика», как и где применяю. Устранение лишних деталей с кадра, резкость, объем и блики.",
              4: "Портфолио Ревю. Рекомендации и свободные вопросы."
            },
            image: "/images/palette.jpg" },
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
.day-description {
  display: flex;
  flex-direction: column;
  /* justify-content: center; */
}

.description-image-class {
  display: flex;
  justify-content: center;
  height: 15vh;
  width: 100%;
  margin: 4vh 0
}

.description-image-class img {
  height: 100%;
  margin: 0 !important
}

.bookImage {
  position: absolute;
  height: 15%;
  top: 20vh;
}

.education-container {
  position: relative;
  display: flex;
  flex-direction: row;
  /* background-size: cover;
  background-image: url('/images/edbg2.jpg'); */
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
  text-align: left;
}

.days-content {
  font-size: 1.9vh
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
  .education-right-part {
    justify-content: center;
  }
  .description-image-class {
    height: 10vh;
    margin-bottom: 2vh;
    margin-top: 0
  }
}
</style>

<template>
  <section id='ОБУЧЕНИЕ' class='course-sect'>
    <div class="education-container">

      <div ref='leftPart' class="education-left-part">
        <p>индивидуальное обучение</p>
        <div ref='daysContainer' class="days-container">
          <button @click='openDescription(index, day.description)' :key='day.id' v-for='(day, index) in educationDays'>{{ day.number }}</button>
        </div>
      </div>

      <div ref='rightPart' class="education-right-part">
        <span class='close-sidebar-btn' @click='closeDescription'><i class="fas fa-times"></i></span>
        <div ref='daysContent' class="days-content"></div>
      </div>

    </div>
  </section>
</template>

<script>
export default {
  name: 'EducationComponent',

  data() {
    return {
      educationDays: {
        1: {number: 'УСЛОВИЯ', description: '- Обучение проходит в формате online-лекции, через SKYPE.<br>- Продолжительность одной лекции: 2 - 2.5 часа <br>- Стоимость обучения - 7500 рублей.<br>*Для бронирования даты необходимо внести задаток в размере - 2500 рублей.'},
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
    openDescription(refIndex, description) {
      for (let ref in this.$refs) {
        if (this.$refs[ref][0]) {
          let refItemStyle = this.$refs[ref][0].style;
          refItemStyle.opacity='0';
          refItemStyle.pointerEvents = 'none'
        }
      }

      if (window.screen.width < 950) {
        this.$refs.leftPart.style.display = 'none';
        this.$refs.rightPart.style.width = '100%';
      }

      this.$refs.daysContainer.style.width = '100%'
      this.$refs.leftPart.style.width = '50%';
      this.$refs.rightPart.style.opacity = '1';
      this.$refs.rightPart.style.pointerEvents = 'all';
      this.$refs.daysContent.innerHTML = description;
    },
    closeDescription() {
      if (window.screen.width < 950) {
        this.$refs.leftPart.style.display = 'flex'
      } else {
        this.$refs.daysContainer.style.width = '50%'
      }
      this.$refs.leftPart.style.width = '100%'
      this.$refs.rightPart.style.opacity = '0'
      this.$refs.rightPart.style.pointerEvents = 'none'

    }
  }
}
</script>

<style media="screen">
.education-container {
  position: relative;
  display: flex;
  flex-direction: row;
  width: 90%;
  margin-left: 5%;
  top: 10vh;
  height: 80vh;
}

.education-left-part {
  display: flex;
  flex-direction: column;
  width: 100%;
  justify-content: center;
  align-items: center;
  text-align: justify;
  color: black;
  transition: 0.2s
  /* background: linear-gradient(to bottom, rgba(2, 2, 2, 0.2), rgba(0, 0, 0, 0.2)) */
}

.education-left-part p {
  font-size: 25px;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.course-description {
  margin-bottom: 20px;
}

.days-container {
  width: 50%;
  margin: 20px 0;
  display: flex;
  justify-content: space-between;
  letter-spacing: 2px
}

.days-container button{
  background: none;
  border: none;
  outline: none;
  padding: 2px 0px;
  font-size: 20px;
  letter-spacing: 2px;
  transition: 0.2s;
  will-change: transform;
}

.days-container button:hover {
  transform: scale(1.1, 1.1);
}
.days-container button:focus {
  outline: none;
}

.education-btn {
  background: none;
  outline: none;
  border: none;
  /* padding: 5px; */
  transition: 0.2s
}

.education-btn:focus {
  outline: none;
  transform: scale(1.1, 1.1);
}

.education-right-part {
  position: absolute;
  width: 50%;
  background-color:white;
  opacity: 0;
  height: 100%;
  transition: all 0.5s;
  right: 0 !important;
  left: auto;
  pointer-events: none;
  color: black;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.days-content {
  text-align: justify;
  width: 70%;
  font-size: 18px;
}

@media screen and (max-width: 1100px) {
  .education-left-part p {
    font-size: 20px;
  }

  .days-container button{
    background: none;
    border: none;
    outline: none;
    padding: 2px 0px;
    font-size: 15px;
    letter-spacing: 2px;
    transition: 0.2s;
    will-change: transform;
  }
}
@media screen and (max-width: 790px) {
  .education-left-part p {
    font-size: 15px;
    letter-spacing: 1px
  }

  .days-container button{
    background: none;
    border: none;
    outline: none;
    padding: 2px 0px;
    font-size: 11px;
    letter-spacing: 1px;
    transition: 0.2s;
    will-change: transform;
  }
}
@media screen and (max-width: 560px) {
  .education-left-part p {
    font-size: 12px;
    letter-spacing: 1px
  }

  .days-container button{
    background: none;
    border: none;
    outline: none;
    padding: 2px 0px;
    font-size: 9px;
    letter-spacing: 1px;
    transition: 0.2s;
    will-change: transform;
  }

  .days-container {
    width: 90%
  }

  .days-content {
    width: 80%;
    font-size: 12px
  }

}
</style>

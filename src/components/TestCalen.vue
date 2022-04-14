<template>
  <div id="testCalen">
    <div class="row row-select">
      <div class="btn btn-left" @click="monthDown">&lsaquo;</div>
      <div id="month-name">
        {{ selectMonthName }}
        <span v-if="selectYear != tecYear">{{ selectYear }}</span>
      </div>
      <div class="btn btn-right" @click="monthUp">&rsaquo;</div>
    </div>
    <div class="row row-days-name">
      <div
        v-for="(day, index) in daysOfWeek"
        :key="'day-name-' + index"
        class="days-name"
        :class="{ 'text-grey': index > 4 }"
      >
        {{ day }}
      </div>
    </div>
    <div class="row row-calendar">
      <div v-for="i in 31" :key="'day-' + i" class="day"></div>
    </div>
    <h2>Текущий год {{ tecYear }}</h2>
    <h2>Выбранный год {{ selectYear }}</h2>
  </div>
</template>

<script>
import moment from "moment";

export default {
  data() {
    return {
      daysOfWeek: [
        "Понедельник",
        "Вторник",
        "Среда",
        "Четверг",
        "Пятница",
        "Суббота",
        "Воскресенье",
      ],
      tecYear: moment().format("YYYY"),
      tecMonthNumber: moment().format("M") - 1,
      selectYear: moment().format("YYYY") || "",
      selectMonthNumber: moment().format("M") - 1 || "",
    };
  },
  mounted() {
    moment.locale("ru");
  },
  computed: {
    selectMonthName() {
      return moment().month(this.selectMonthNumber).format("MMMM");
    },
  },
  methods: {
    monthUp() {
      if (this.selectMonthNumber === 11) {
        this.selectYear++;
        this.selectMonthNumber = 0;
      } else {
        this.selectMonthNumber++;
      }
    },
    monthDown() {
      if (this.selectMonthNumber === 0) {
        this.selectYear--;
        this.selectMonthNumber = 11;
      } else {
        this.selectMonthNumber--;
      }
    },
  },
};
</script>

<style scoped>
#testCalen {
  background-color: #fff;
  border-radius: 16px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
  height: calc(100vh - 48px);
  padding: 16px;
}

/* Строка смены месяца */

.row-select {
  display: flex;
}

.btn {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 32px;
  /* border: 1px solid grey; */
  padding: 0 8px 0 8px;
}

#month-name {
  /* border: 1px solid darkgrey; */
  font-size: 20px;
  font-weight: bold;
  padding: 10px 4px 0 4px;
  text-transform: uppercase;
}

/* Строка дней недели */

.row-days-name {
  display: flex;
  margin-top: 16px;
}

.days-name {
  /* border: 1px solid darkgrey; */
  font-size: 12px;
  font-weight: bold;
  /* height: 24px; */
  padding: 4px 4px;
  text-align: right;
  text-transform: uppercase;
  width: calc(100% / 7); /* 14.28%; */
}

/* Строка календаря */

.row-calendar {
  display: flex;
  flex-wrap: wrap;
}

.day {
  border: 1px solid darkgrey;
  height: 64px;
  margin: 1px;
  width: calc((100% - 14px) / 7);
}

/* Вспомогательные классы */
.text-grey {
  color: #d5d5d5;
}
</style>
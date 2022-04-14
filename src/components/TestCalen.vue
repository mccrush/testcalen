<template>
  <div id="testCalen">
    <!-- Смена месяца -->
    <div class="row row-select">
      <div class="btn btn-left" @click="monthDown">&lsaquo;</div>
      <div id="month-name">
        {{ getSelectMonthName }}
        <span v-if="selectYear !== tecYear">{{ selectYear }}</span>
      </div>
      <div class="btn btn-right" @click="monthUp">&rsaquo;</div>
    </div>
    <!-- Конец Смена месяца -->

    <!-- Дни недели -->
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
    <!-- Конец Дни недели -->

    <!-- Календарь -->
    <div class="row row-calendar">
      <div
        v-for="i in getDayOfWeek(selectYear, selectMonthNumber, 1) - 1"
        :key="'day-before-' + i"
        class="day border-grey"
        :class="{
          'bg-grey text-darkgrey':
            (selectMonthNumber <= tecMonthNumber && selectYear <= tecYear) ||
            selectYear < tecYear,
          'day-height-6': getNumberOfRows === 6,
          'day-height-5': getNumberOfRows === 5,
          'text-purpur':
            getDayOfWeek(
              selectYear,
              selectMonthNumber - 1,
              getDaysInMonth(selectYear, selectMonthNumber) -
                getDayOfWeek(selectYear, selectMonthNumber, 1) +
                i +
                1
            ) >= 6,
        }"
      >
        {{
          getDaysInMonth(selectYear, selectMonthNumber) -
          getDayOfWeek(selectYear, selectMonthNumber, 1) +
          i +
          1
        }}
      </div>
      <div
        v-for="i in getDaysInMonth(selectYear, selectMonthNumber + 1)"
        :key="'day-' + i"
        class="day border-grey"
        :class="{
          'bg-grey text-darkgrey':
            (i < tecDate &&
              selectMonthNumber === tecMonthNumber &&
              selectYear <= tecYear) ||
            (selectMonthNumber < tecMonthNumber && selectYear <= tecYear) ||
            selectYear < tecYear,
          'border-darkgrey text-green':
            i === tecDate &&
            selectMonthNumber === tecMonthNumber &&
            selectYear === tecYear,
          'day-height-6': getNumberOfRows === 6,
          'day-height-5': getNumberOfRows === 5,
          'text-purpur': getDayOfWeek(selectYear, selectMonthNumber, i) >= 6,
        }"
      >
        {{ i }}
      </div>
      <div
        v-for="i in 7 -
        getDayOfWeek(
          selectYear,
          selectMonthNumber,
          getDaysInMonth(selectYear, selectMonthNumber + 1)
        )"
        :key="'day-after-' + i"
        class="day border-grey"
        :class="{
          'bg-grey text-darkgrey':
            (selectMonthNumber < tecMonthNumber && selectYear <= tecYear) ||
            selectYear < tecYear,
          'day-height-6': getNumberOfRows === 6,
          'day-height-5': getNumberOfRows === 5,
          'text-purpur':
            getDayOfWeek(selectYear, selectMonthNumber + 1, i) >= 6,
        }"
      >
        {{ i }}
      </div>
    </div>
    <!-- Конец Календарь -->
    <h4>
      Дней в выбраном месяце
      {{ getDaysInMonth(selectYear, selectMonthNumber + 1) }}
    </h4>
    <h4>День недели 1 числа {{ getNumberOfRows }}</h4>
    <h4>Текущий год {{ tecYear }}</h4>
    <h4>Выбранный год {{ selectYear }}</h4>
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
      tecYear: moment().get("year"),
      tecMonthNumber: moment().get("month"),
      tecDate: moment().get("date"),
      selectYear: moment().get("year") || "",
      selectMonthNumber: moment().get("month") || "",
    };
  },
  mounted() {
    moment.locale("ru");
  },
  computed: {
    getSelectMonthName() {
      return moment().month(this.selectMonthNumber).format("MMMM");
    },
    getNumberOfRows() {
      if (this.getDayOfWeek(this.selectYear, this.selectMonthNumber, 1) >= 6) {
        return 6;
      } else {
        return 5;
      }
    },
  },
  methods: {
    getDayOfWeek(year, month, date) {
      if (new Date(year, month, date).getDay() === 0) {
        return 7;
      } else {
        return new Date(year, month, date).getDay();
      }
    },
    getDaysInMonth(year, month) {
      if (month === 0) {
        month = 12;
        year--;
      }
      return moment(year + "-" + month, "YYYY-MM").daysInMonth();
    },
    monthUp() {
      console.log("Clik Up");
      if (this.selectMonthNumber === 11) {
        this.selectYear++;
        this.selectMonthNumber = 0;
      } else {
        this.selectMonthNumber++;
      }
    },
    monthDown() {
      console.log("Clik Down");
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
  padding: 0 8px 0 8px;
}

#month-name {
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
  font-size: 12px;
  font-weight: bold;
  padding: 4px;
  text-align: right;
  text-transform: uppercase;
  width: calc(100% / 7);
}

/* Строка календаря */
.row-calendar {
  display: flex;
  flex-wrap: wrap;
}

.day {
  border: 1px solid darkgrey;
  font-size: 12px;
  font-weight: bold;
  margin: 1px;
  padding: 4px;
  text-align: right;
  width: calc((100% - 14px) / 7);
}

.day-height-5 {
  height: calc((100vh - 158px) / 5);
}

.day-height-6 {
  height: calc((100vh - 158px) / 6);
}

/* Вспомогательные классы */
.text-grey {
  color: #d5d5d5;
}

.text-darkgrey {
  color: #607d8b;
}

.text-purpur {
  color: #3f51b5;
}

.text-green {
  color: #8bc34a;
}

.border-grey {
  border: 1px solid #d5d5d5;
}

.border-darkgrey {
  border: 1px solid #607d8b;
}

.bg-grey {
  background-color: #d5d5d5;
}
</style>
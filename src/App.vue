<template>
  <TestCalen :events="events" />
</template>

<script>
import TestCalen from "./components/TestCalen.vue";

export default {
  name: "App",
  components: {
    TestCalen,
  },
  data() {
    return {
      events: [
        {
          id: 1,
          title: "Отправить посылку Елене",
          date: "2022-04-12T12:39",
          type: "easy",
        },
        {
          id: 2,
          title: "Завершить вторую главу дипломной работы",
          date: "2022-04-23T10:10",
          type: "hard",
        },
        {
          id: 3,
          title: "Обновить логотип на сайте строительных инструментов",
          date: "2022-04-16T15:20",
          type: "medium",
        },
        {
          id: 4,
          title: "Выяснить, почему у соседей трава зеленее",
          date: "2022-04-16T10:30",
          type: "hard",
        },
        {
          id: 5,
          title:
            "Подготовить отчет за прошлую неделю и отправить на электронную почту",
          date: "2022-04-19T16:45",
          type: "medium",
        },
        {
          id: 6,
          title: "Выполнить лабораторные работы по начертательной геометрии",
          date: "2022-04-129T09:10",
          type: "hard",
        },
        {
          id: 7,
          title: "Собрать сумку для командировки",
          date: "2022-04-15T12:40",
          type: "easy",
        },
        {
          id: 8,
          title: "Выполнить тестовое задание для Frontend",
          date: "2022-04-15T10:05",
          type: "medium",
        },
      ],
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  background-color: #f5f5f5;
  color: #2c3e50;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  /* -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; */
  line-height: 1;
  padding: 24px;
}
</style>

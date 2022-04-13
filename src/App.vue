<template>
  <TestCalen />
</template>

<script>
import TestCalen from "./components/TestCalen.vue";

export default {
  name: "App",
  components: {
    TestCalen,
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

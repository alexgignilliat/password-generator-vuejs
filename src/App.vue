<template>
  <div id="app">
    <PasswordGenerator msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import PasswordGenerator from "./components/PasswordGenerator.vue";

export default {
  name: "App",
  components: {
    PasswordGenerator,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  padding: 0 35%;
  background-color: #2c3e5000;
}

body {
  background-color: rgba(255, 0, 0, 0);
}

html {
  background-color: #736d964d;
}
</style>

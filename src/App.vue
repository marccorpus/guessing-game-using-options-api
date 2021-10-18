<template>
  <div id="app">
    <GuessingGame />
  </div>
</template>

<script>
import GuessingGame from "./components/GuessingGame.vue";

export default {
  components: {
    GuessingGame,
  },
};
</script>

<style>
body {
  background: linear-gradient(to right, #7f53ac, #657ced);
  font-family: "Quicksand", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#app {
  margin-top: 40px;
  text-align: center;
}
.btn {
  border-color: #663399 !important;
  border-radius: 5px;
  background-color: #663399 !important;
  color: #fff;
}
</style>

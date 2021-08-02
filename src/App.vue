<template>
  <div id="app">
    <h1>Pomodoro App</h1>
    <img src="./assets/pomodoro.jpg" />
    <Timer />
  </div>
</template>

<script>
import Timer from "./components/Timer";
export default {
  name: "app",
  components: {
    Timer
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

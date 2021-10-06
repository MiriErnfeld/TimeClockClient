<template>
  <div id="app">
    <DigitalClock></DigitalClock>
    <Users></Users>

  </div>
</template>

<script>
import Users from "./components/Users.vue";
import DigitalClock from "./components/Clock.vue";

export default {
  name: "App",
  components: {
    DigitalClock,
    Users,
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
}
</style>

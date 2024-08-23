<template>
  <div class="max-w-1 max-h-1 flex flex-row justify-center">
    <img alt="Vue logo" src="./assets/just-do-it.png" id="logo" />
  </div>
  <Task msg="Just Do It" />
</template>

<script>
import Task from "./components/Task.vue";

export default {
  name: "App",
  components: {
    Task,
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
#logo {
  max-width: 50px;
}
</style>

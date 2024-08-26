<template>
  <div class="background">
    <div class="color_option">
      <button
        class="flat-selector button-theme"
        @click="handleColorChange('flat')"
      /><button
        class="light-selector button-theme"
        @click="handleColorChange('light')"
      /><button
        class="dark-selector button-theme"
        @click="handleColorChange('dark')"
      />
    </div>
    <div class="max-w-1 max-h-1 flex flex-row justify-center">
      <img alt="Vue logo" src="./assets/just-do-it.png" id="logo" />
    </div>
    <Task msg="Just Do It" :color="color" />
  </div>
</template>

<script>
import Task from "./components/Task.vue";

export default {
  name: "App",
  data() {
    return {
      color: "flat",
    };
  },
  components: {
    Task,
  },
  methods: {
    handleColorChange(newColor) {
      this.color = newColor;
    },
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
  margin: -8px;
}
#logo {
  max-width: 50px;
}
.color_option {
  justify-content: start;
  margin-bottom: 5px;
  padding-top: 10px;
  display: flex;
  gap: 10px;
}
.background {
  background-image: linear-gradient(100deg, #575656, #062e3f);
  color: #ffdfdb;
  height: 100vh;
}
.button-theme {
  border: 1px solid #d1dae3;
  border-radius: 100%;
  height: 35px;
  margin: 0 8px;
  transition: tranform 150ms ease-in-out, box-shadow 200ms ease-in-out;
  width: 35px;
}
.button-theme:hover {
  box-shadow: white 0 0 8px;
  cursor: pointer;
}
.button-theme:active {
  transform: scale(0.95);
}
.light-selector {
  background-image: linear-gradient(100deg, #d4f1ff, #ffffff);
}
.flat-selector {
  background-image: linear-gradient(100deg, #575656, #062e3f);
}
.dark-selector {
  background-image: linear-gradient(100deg, #001214, #001f29);
}
</style>

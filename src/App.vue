<template>
  <div :class="backgroundClass">
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
      <img alt="just do it" src="./assets/just-do-it.png" :class="logoClass" />
      <img
        alt="just do it"
        src="./assets/just-do-it-white.png"
        :class="logoClass2"
      />
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
  computed: {
    backgroundClass() {
      return {
        background: this.color === "flat",
        backgroundLight: this.color === "light",
        backgroundDark: this.color === "dark",
      };
    },
    logoClass() {
      return {
        blackLogo: this.color === "flat",
        defaultLogo: this.color === "light",
        hidden: this.color === "dark",
      };
    },
    logoClass2() {
      return {
        hide: this.color === "flat",
        hidden: this.color === "light",
        whiteLogo: this.color === "dark",
      };
    },
    imageSource() {
      switch (this.color) {
        case "flat":
          return "/img/just-do-it.b0253281.png";
        case "dark":
          return "/img/just-do-it-white.afbd0736.png";
        case "light":
          return "/img/just-do-it.b0253281.png";
        default:
          return "/img/just-do-it.b0253281.png";
      }
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
.blackLogo {
  width: 50px;
}
.hide {
  display: none;
}
.hidden {
  display: none;
}
.defaultLogo {
  width: 50px;
}
.whiteLogo {
  width: 60px;
  margin-top: -16px;
  margin-bottom: -24px;
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
  transition: 0.3s linear;
  height: 100vh;
}
.backgroundLight {
  background-image: linear-gradient(100deg, #d4f1ff, #ffffff);
  color: #1a150e;
  transition: 0.3s linear;
  height: 100vh;
}
.backgroundDark {
  background-image: linear-gradient(100deg, #001214, #001f29);
  color: white;
  transition: 0.3s linear;
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
@media only screen and (max-width: 600px) {
  .color_option {
    justify-content: start;
    margin-bottom: 5px;
    padding-top: 10px;
    display: flex;
    gap: 0px;
  }
  .button-theme {
    border: 1px solid #d1dae3;
    border-radius: 100%;
    height: 25px;
    margin: 0 6px;
    transition: tranform 150ms ease-in-out, box-shadow 200ms ease-in-out;
    width: 25px;
  }
}
</style>

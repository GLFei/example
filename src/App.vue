<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import HelloWorld from "./components/Calc.vue";
// import HelloWorld from "./components/Clock.vue";
import HelloWorld from "./components/Keyboard.vue";
// import HelloWorld from "./components/Halloween";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
};
</script>

<style>
body,
div {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>

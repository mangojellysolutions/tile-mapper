<template>
  <div id="app">
    <Container msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import Container from "./components/Container.vue";

export default {
  name: "App",
  components: {
    Container
  }
};
</script>

<style>
#app {
}
body {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0px;
  padding: 0px;
  height: 100%;
  width:100%;
  position: absolute;
}
</style>

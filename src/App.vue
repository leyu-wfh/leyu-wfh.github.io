<template>
  <div id="app">
    <Scatter />
    <br />
    <FxFake />
    <FxApi />
  </div>
</template>

<script>
import Scatter from "./components/Scatter";
import FxFake from "./components/FxFake";
import FxApi from "./components/FxAPI";

export default {
  name: "App",
  components: {
    Scatter,
    FxFake,
    FxApi
  }
};
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>

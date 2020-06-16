<template>
  <div id="app">
    <Header />
    <router-view></router-view>
  </div>
</template>

<script>
import Header from "./components/Header.vue";

export default {
  components: {
    Header
  }
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0px;
  padding: 0px;
}

body {
  background-color: #92bde7;
  color: #485e74;
  line-height: 1.6;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  padding: 0;
  overflow: hidden;
}

.app {
  max-width: 1170px;
  margin-left: auto;
  margin-right: auto;
  padding: 1em;
}
</style>

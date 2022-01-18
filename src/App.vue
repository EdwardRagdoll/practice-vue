<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <DatePicker /> -->
    <!-- <Layout /> -->
    <GrandPa />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import DatePicker from './components/element/el-date-picker.vue'
// import Layout from './components/element/el-layout.vue'
import GrandPa from "@/views/GrandPa.vue"
export default {
  name: 'App',
  components: {
    // HelloWorld,
    // DatePicker,
    // Layout,
    GrandPa
  }
}
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

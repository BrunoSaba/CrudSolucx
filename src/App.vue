<template>
  <div id="app">
    <deliveryReport/>
  </div>
</template>

<script>
import DeliveryReport from './components/DeliveryReport.vue'


export default {
  name: 'App',
  components: {
    DeliveryReport
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

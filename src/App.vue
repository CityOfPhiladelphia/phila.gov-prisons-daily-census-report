<template>
  <div id="vue-app">
    <DailyCensus />
  </div>
</template>

<script>
import DailyCensus from './components/DailyCensus.vue'

export default {
  name: 'App',
  components: {
    DailyCensus,
  }
}
</script>

<style>
#vue-app {
  /* width: 70rem; */
  margin: 0 auto;
}
</style>

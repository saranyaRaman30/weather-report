<template>
  <div id="app">
    <weather></weather>
<!--     <test></test> -->
  </div>
</template>

<script>
import weather from './components/weather.vue'
// import test from './components/test.vue'
export default {
  name: 'app',
   components:{
    weather
  }
  
}
</script>

<template>
  <div id="app">
    
    <LayPush></LayPush>
   
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import LayPush from './components/LayPush.vue';





export default {
  name: 'app',
  components: {
    HelloWorld,
    LayPush,
  
  }}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
 
  
}
</style>

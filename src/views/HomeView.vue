<template>
  <div class="home">
    
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <LayPush></LayPush>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import LayPush from '@/components/LayPush.vue';


export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    LayPush
    
    
}
}
</script>

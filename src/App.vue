<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld/> -->
   <RandomArt/>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import RandomArt from './components/RandomArt.vue';

export default {
  name: 'App',
  components: {
    // HelloWorld,
    RandomArt
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

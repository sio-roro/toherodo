<template>
  <div id="app">
    
    <Dnd1 />
  </div>
</template>

<script>

import Dnd1 from './components/dnd1.vue'


export default {
  name: 'App',
  components: {
    Dnd1
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
  background: #484848;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: scroll;
}
</style>

<template>
  <div id="app">
    
    <Dnd1 />
  </div>
</template>

<script>

import Dnd1 from './components/dnd1.vue'

var express = require('express');
var path = require('path');
var serveStatic = require('serve-static');
app = express();
app.use(serveStatic(__dirname + "/dist"));
var port = process.env.PORT || 5000;
app.listen(port);
console.log('server started '+ port);


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

<template>
  <div class="hello">
    <div ref='test' id='test'></div>
  </div>
</template>

<script>
import Vue from 'vue'
var Marzipano = require('../../node_modules/marzipano')
Vue.use(Marzipano)

export default {
  name: 'HelloWorld',
  mounted: function () {
    const element = document.getElementById('test')
    console.log(element)
    const viewer = new Marzipano.Viewer(element)
    console.log(viewer)
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

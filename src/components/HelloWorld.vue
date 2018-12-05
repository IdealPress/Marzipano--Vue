<template>
  <div class="hello">
    <div id='pano'></div>
  </div>
</template>

<script>
import Vue from 'vue'
var Marzipano = require('../../node_modules/marzipano')
Vue.use(Marzipano)

export default {
  name: 'HelloWorld',

  mounted: function () {
    var viewer = new Marzipano.Viewer(document.getElementById('pano'))
    console.log(viewer)
    var source = Marzipano.ImageUrlSource.fromString('//www.marzipano.net/media/cubemap/{f}.jpg')
    var geometry = new Marzipano.CubeGeometry([{ tileSize: 1024, size: 1024 }])
    var limiter = Marzipano.RectilinearView.limit.traditional(4096, 100 * Math.PI / 180)
    var view = new Marzipano.RectilinearView(null, limiter)
    var scene = viewer.createScene({
      source: source,
      geometry: geometry,
      view: view,
      pinFirstLevel: true
    })
    scene.switchTo()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
  -webkit-user-drag: none;
  -webkit-touch-callout: none;
  -ms-content-zooming: none;
}

html, body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
  overflow: hidden;
  font-family: helvetica, sans-serif;
}

#pano {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>

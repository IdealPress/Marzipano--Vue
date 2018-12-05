<template>
  <div class="hello">
    <div id='pano'></div>
    <div id='info'><a href="/"><div class='info'></div></a></div>
  </div>
</template>

<script>
import Vue from 'vue'
var Marzipano = require('../../node_modules/marzipano')
Vue.use(Marzipano)

export default {
  name: 'HelloWorld',

  mounted: function () {
    // Create viewer.
    var viewer = new Marzipano.Viewer(document.getElementById('pano'))
    // Create source.
    var source = Marzipano.ImageUrlSource.fromString(
      '//waf.not-working.co.uk/unite-students/tiles/commonroom/{z}/{f}/{y}/{x}.jpg',
      { cubeMapPreviewUrl: '//waf.not-working.co.uk/unite-students/tiles/commonroom/preview.jpg' })

    // Create geometry.
    var geometry = new Marzipano.CubeGeometry([
      { tileSize: 256, size: 256, fallbackOnly: true },
      { size: 512, tileSize: 512 },
      { size: 1024, tileSize: 512 },
      { size: 2048, tileSize: 512 }
    ])
    // Create view.
    var limiter = Marzipano.RectilinearView.limit.traditional(2048, 120 * Math.PI / 180)
    var view = new Marzipano.RectilinearView(null, limiter)
    // Create scene.
    var scene = viewer.createScene({
      source: source,
      geometry: geometry,
      view: view,
      pinFirstLevel: true
    })
    // Autorotate function
    var autorotate = Marzipano.autorotate({
      yawSpeed: 0.1,
      targetPitch: 0,
      targetFov: Math.PI / 2
    })
    // Autorotate will start after 3s of idle time
    viewer.setIdleMovement(3000, autorotate)
    viewer.startMovement(autorotate)
    // Display scene.
    scene.switchTo({ transitionDuration: 0 })
    scene.hotspotContainer().createHotspot(document.querySelector('#info'), { yaw: -3.85, pitch: 0.38 })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang='scss'>
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
  width: 1024px;
  height: 600px;
  padding: 0;
  margin: 0;
  overflow: hidden;
  font-family: helvetica, sans-serif;
}

#pano {
  position: absolute;
  top: 0;
  left: 0;
  width: 1024px;
  height: 600px;
}

#info{
  width: 50px;
  height: 50px;
  cursor: pointer;
}

.info {
  width: 100%;
  height: 100%;
  background-position: center;
  background-size: cover;
  background-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz48c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IiB2aWV3Qm94PSIwIDAgNDYgNDUiIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDQ2IDQ1OyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSI+PHN0eWxlIHR5cGU9InRleHQvY3NzIj4uc3Qwe2ZpbGw6I0ZGRkZGRjt9PC9zdHlsZT48cGF0aCBjbGFzcz0ic3QwIiBkPSJNNDQuNSwyMi4yYzAtMTItOS43LTIxLjctMjEuNy0yMS43UzEsMTAuMiwxLDIyLjJjMCwxMiw5LjcsMjEuOCwyMS43LDIxLjhTNDQuNSwzNC4yLDQ0LjUsMjIuMnogTTIwLjcsMjkuNGwtOC04Yy0wLjYtMC42LTAuOS0xLjQtMC45LTIuMXMwLjMtMS41LDAuOS0yLjFjMS4yLTEuMiwzLjEtMS4yLDQuMiwwbDUuOSw1LjhsNS45LTUuOWMxLjItMS4yLDMuMS0xLjIsNC4yLDBjMS4yLDEuMiwxLjIsMy4xLDAsNC4ybC04LDhDMjMuOCwzMC41LDIxLjksMzAuNSwyMC43LDI5LjR6Ii8+PC9zdmc+);
}
</style>

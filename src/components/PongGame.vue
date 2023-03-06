<script lang="ts">
import * as PIXI from 'pixi.js'

export default {
  methods: {
    initPixi: async () => {
      const canvas = document.getElementById('pixi')

      if (canvas) {
        const app = new PIXI.Application({
          width: window.innerWidth / 2,
          height: window.innerHeight / 2,
          antialias: true,
          transparent: true,
          view: canvas
        })

        // load the texture we need
        const texture = await PIXI.Assets.load('src/assets/logo.svg')

        // This creates a texture from a 'bunny.png' image
        const bunny = new PIXI.Sprite(texture)

        // Setup the position of the bunny
        bunny.x = app.renderer.width / 2
        bunny.y = app.renderer.height / 2

        // Rotate around the center
        bunny.anchor.x = 1
        bunny.anchor.y = 0

        // Add the bunny to the scene we are building
        app.stage.addChild(bunny)

        // Listen for frame updates
        app.ticker.add(() => {
          // each frame we spin the bunny around a bit
          bunny.rotation += 0.01
        })
      }
    }
  },

  mounted() {
    this.initPixi()
  },

  beforeUnmount() {
    // TODO CLOSE OPENGL INSTANCE
    const canvas = document.getElementById('pixi')
    if (canvas) {
      canvas.remove()
    }
  }
}
</script>

<template>
  <div class="greetings">
    <canvas id="pixi"></canvas>
  </div>
</template>

<style scoped>
.greetings {
  text-align: center;
}
</style>

<template>
  <div class="dashboard bg-wrapper bg-gradient">
    <nav>
      <DashboardNavbar />
    </nav>

    <div class="canvas-wrapper" id="canvasContainer">
      <div class="toolbar">
          <div class="input-group mb-3">
            <input ref= "imgInput" accept="image/*" type="file" class="form-control" id="imgUpload" v-on:change="">
            <label class="input-group-text" for="" @click="">Upload</label>
            <button @click="draw">Draw Dot</button>
          </div>
      </div>

      <v-stage ref="stage" :config="config">
        <v-layer @click="draw" ref="layer">
          <v-rect id="canvas" :config="{x:0, y:0, width:400, height: 600, fill: 'white'}"
                  @mousemove="draw" @mousedown="toggleMouseIsDown" @mouseup="toggleMouseIsDown"
                  @touchmove="draw" @touchstart="toggleTouchStart" @touchend="toggleTouchStart"/>
        </v-layer>
      </v-stage>

    </div>
  </div>
</template>

<script>

import {ref} from "vue";
import Konva from "konva";

export default {
  name: "GratitudeBoard",

  setup() {
    const stage = ref()
    const layer= ref()
    const config = {
      width: 400,
      height: 600,
    }


    const mouseX = ref()
    const mouseY = ref()
    const mouseIsDown = ref(false)

    const touchX = ref()
    const touchY = ref()
    const touchStart = ref(false)

    function draw() {
      const mousePos = stage.value.getNode().getPointerPosition()
      const ctx = layer.value.getNode()

      const dot = new Konva.Circle({
        x: mousePos.x,
        y: mousePos.y,
        radius: 5,
        fill: 'black',
      })

      if(mouseIsDown.value) {
        ctx.add(dot)
      }
    }

    function touch() {
      const touchPos = stage.value.getNode().getPointerPosition()
      const ctx = layer.value.getNode()

      const dot = new Konva.Circle({
        x: touchPos.x,
        y: touchPos.y,
        radius: 5,
        fill: 'black'
      })
      
      ctx.preventDefault()
      if(touchStart.value) {
        ctx.add(dot)
      }
    }


    function toggleMouseIsDown(event) {
      event.type === 'mousedown' ? mouseIsDown.value = true : mouseIsDown.value = false
    }

    function toggleTouchStart(TouchEvent) {
      TouchEvent.type === 'touchstart' ? touchStart.value = true : touchStart.value = false
    }

    // function draw(event) {
    //   const ctx = canvas.value.getContext('2d')
    //   let mx = event.offsetX
    //   let my = event.offsetY
    //
    //   if (mouseIsDown.value) {
    //     drawDot(mx, my, ctx)
    //   }
    // }
    //
    // function touch(TouchEvent) {
    //   TouchEvent.preventDefault()
    //   TouchEvent.stopPropagation()
    //
    //   const ctx = canvas.value.getContext('2d')
    //   const canvasPos = canvas.value.getBoundingClientRect()
    //   const touch = TouchEvent.touches[0]
    //   const tx = touch.clientX - canvasPos.x
    //   const ty = touch.clientY - canvasPos.y
    //
    //   if (touchStart.value) {
    //     drawDot(tx, ty, ctx)
    //   }
    // }
   // function getImageURL() {
   //  const file = imgInput.value.files[0]
   //
   //  const reader = new FileReader()
   //  reader.readAsDataURL(file)
   //    reader.onload = () => {
   //      drawImg(reader.result)
   //    }
   // }



      return {
      stage, layer, config, mouseIsDown, mouseX, mouseY, touchStart, touchX, touchY,
      draw, toggleMouseIsDown, touch, toggleTouchStart
      }
    },
  }


</script>

<style scoped>

</style>
<template>
  <div class="dashboard bg-wrapper bg-gradient">
    <nav>
      <DashboardNavbar />
    </nav>

    <div class="canvas-wrapper" id="canvasContainer">
      <div class="toolbar bg-gradient" style="background-color: black">
          <div class="input-group mb-3">
            <input ref= "imgInput" accept="image/*" type="file" class="form-control" id="imgUpload" v-on:change="">
            <label class="input-group-text" for="" @click="drawImg">Upload</label>
          </div>
          <button class="btn btn-info" @click="clear">Clear</button>
      </div>

      <v-stage ref="stage" :config="stageConfig">
        <v-layer @click="draw" ref="layer">
          <v-rect id="canvas" :config="canvasConfig"
                  @mousemove="draw" @mousedown="toggleMouseIsDown" @mouseup="toggleMouseIsDown"
                  @touchmove="touch" @touchstart="toggleTouchStart" @touchend="toggleTouchStart"/>
          <v-image id="uploadedImage" />
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
    const stageConfig = {
      width: 400,
      height: 600,
    }

    const layer= ref()
    const canvasConfig = {
      width: 400,
      height: 600,
      fill: 'lavender'
    }

    const imgInput = ref('')
    const imgUploaded = ref()

    const mouseX = ref()
    const mouseY = ref()
    const mouseIsDown = ref(false)

    const touchX = ref()
    const touchY = ref()
    const touchStart = ref(false)

    function clear() {
      const ctx = layer.value.getNode()
      const children = ctx.children

      for(const child of children.slice(1, children.length)) {
          child.remove()
      }
    }

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

   function drawImg() {
    const ctx = layer.value.getNode()
    const newImage = new window.Image()
    const file = imgInput.value.files[0]
    const reader = new FileReader()

    reader.readAsDataURL(file)
      reader.onload = () => {
        newImage.src = reader.result
        imgUploaded.value = new Konva.Image({
          image: newImage,
          width: 100,
          height: 100,
          draggable: true,
        })
        ctx.add(imgUploaded.value)
       }

   }

    function toggleMouseIsDown(event) {
      event.type === 'mousedown' ? mouseIsDown.value = true : mouseIsDown.value = false
    }

    function toggleTouchStart(TouchEvent) {
      TouchEvent.type === 'touchstart' ? touchStart.value = true : touchStart.value = false
    }

    return {
    stage, layer, stageConfig, imgInput, mouseIsDown, mouseX, mouseY, touchStart, touchX, touchY, canvasConfig, imgUploaded,
    draw, toggleMouseIsDown, touch, toggleTouchStart, clear, drawImg,
      }
    },
  }


</script>

<style scoped>

</style>
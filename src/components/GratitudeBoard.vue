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
        <button class="btn btn-info" @tap="click" @click="edit">Edit</button>
      </div>

      <v-stage ref="stage" :config="stageConfig">
        <v-layer ref="layer">
          <v-rect ref="canvas" :config="canvasConfig" @click="click" @tap="click"
                  @mousemove="draw" @mousedown="toggleMouseIsDown" @mouseup="toggleMouseIsDown"
                  @touchmove="touch" @touchstart="toggleTouchStart" @touchend="toggleTouchStart"/>
<!--          <v-circle ref="circle" @click="click" @tap="click" :config="{x: 100, y: 100, radius: 50, fill: 'black', name: 'circle'}" />-->
          <v-image @click="click" @tap="click" ref="imgUploaded" :config="standby === false ? {image: imgUploaded.value} : null"/>
          <v-transformer ref="transformer"/>
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
      name: 'stage',
      width: 400,
      height: 600,
    }

    const layer= ref()
    const canvas = ref()
    const canvasConfig = {
      name: 'canvas',
      width: 400,
      height: 600,
      fill: 'lavender'
    }

    const imgInput = ref()
    const imgUploaded = ref()
    const standby = ref(true)

    const circle = ref()

    const transformer = ref()

    const mouseX = ref()
    const mouseY = ref()
    const mouseIsDown = ref(false)

    const touchX = ref()
    const touchY = ref()
    const touchStart = ref(false)


    function getStageNode() {
      return stage.value.getNode()
    }

    function getLayerNode() {
      return layer.value.getNode()
    }

    function getTransformerNode() {
      return transformer.value.getNode()
    }


    function clear() {
      const children = getLayerNode().children

      for(const child of children.slice(1, children.length)) {
          child.remove()
      }
    }

    function edit() {
      const shape = getStageNode().find('.myImage')
      getTransformerNode().nodes([shape[0]])
      console.log(shape[0])
    }

    function draw() {
      const mousePos = getStageNode().getPointerPosition()

      const dot = new Konva.Circle({
        x: mousePos.x,
        y: mousePos.y,
        radius: 5,
        fill: 'black',
      })

      if(mouseIsDown.value) {
        getLayerNode().add(dot)
      }
    }

    function touch() {
      const touchPos = getStageNode().getPointerPosition()

      const dot = new Konva.Circle({
        x: touchPos.x,
        y: touchPos.y,
        radius: 5,
        fill: 'black'
      })

      getLayerNode().preventDefault()
      if(touchStart.value) {
        getLayerNode().add(dot)
      }
    }

   function drawImg() {
    const file = imgInput.value.files[0]
    const reader = new FileReader()
    const newImage = new window.Image()

    reader.readAsDataURL(file)
      reader.onload = () => {
        newImage.src = reader.result

        imgUploaded.value = new Konva.Image({
          image: newImage,
          name: 'myImage',
          x: 100,
          y: 100,
          width: 100,
          height: 100,
          draggable: true,
          listening: true,
        })
        console.log(imgUploaded.value)
        getLayerNode().add(imgUploaded.value)
        getTransformerNode().nodes([imgUploaded.value])
       }
        standby.value = false
   }

    function toggleMouseIsDown(event) {
      event.type === 'mousedown' ? mouseIsDown.value = true : mouseIsDown.value = false
    }

    function toggleTouchStart(TouchEvent) {
      TouchEvent.type === 'touchstart' ? touchStart.value = true : touchStart.value = false
    }

    function click(event) {
      const shape = getStageNode().find('.myImage')
      if(event.target.name() === 'canvas') {
        getTransformerNode().nodes([])
      }
      else if(event.target.name() === 'circle') {
        getTransformerNode().nodes([circle.value.getNode()])
      }
      else if (event.target.name() === shape[0].name()) {
        console.log(event.type)
        getTransformerNode().nodes([shape[0]])
      }

    }

    return {
    stage, layer, canvas, stageConfig, imgInput, standby, mouseIsDown, mouseX, mouseY, touchStart, touchX, touchY,
    canvasConfig, imgUploaded, transformer, circle,
    draw, toggleMouseIsDown, touch, toggleTouchStart, clear, drawImg, click, edit,
      }
    },
  }


</script>

<style scoped>

</style>
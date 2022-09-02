<template>
  <div class="dashboard bg-wrapper bg-gradient">
    <nav>
      <DashboardNavbar />
    </nav>

    <div class="canvas-wrapper">
      <div class="toolbar">
        <div class="container-fluid">
          <div class="input-group mb-3">
            <input type="file" class="form-control" id="imgUpload">
            <label class="input-group-text" for="imgUpload">Upload</label>
          </div>
        </div>
      </div>

      <button @click="clearBoard">Clear</button>

      <div>
        Mouse x: {{mouseX}}, Mouse y: {{mouseY}}
      </div>

      <canvas ref="board" width="375" height="600" v-on:touchstart="draw" @touchstart="toggleMouseIsDown" @touchend="toggleMouseIsDown">
        This is a canvas
      </canvas>
    </div>
  </div>
</template>

<script>

import {onMounted, onUpdated, reactive, ref} from "vue";

export default {
  name: "GratitudeBoard",

  setup() {

    const board = ref(null)
    const mouseX = ref()
    const mouseY = ref()
    const mouseIsDown = ref(false)


    function toggleMouseIsDown(event) {
      event.type === 'touchstart' ? mouseIsDown.value = true : mouseIsDown.value = false
      // mouseIsDown.value = !mouseIsDown.value
    }

    function clearBoard() {
      const ctx = board.value.getContext('2d')
      ctx.clearRect(0, 0, 800, 800)
    }

    function getMouseCoords(event) {
      mouseX.value = event.offsetX
      mouseY.value = event.offsetY
    }

    function draw(event) {
      const ctx = board.value.getContext('2d')
      getMouseCoords(event)
      let mx = event.offsetX
      let my = event.offsetY


        ctx.beginPath()
        ctx.arc(mx, my, 10, 0 , 360 )
        ctx.fill()

    }

    return {board, draw, clearBoard, toggleMouseIsDown, mouseIsDown, mouseX, mouseY}
  }
}


</script>

<style scoped>

</style>
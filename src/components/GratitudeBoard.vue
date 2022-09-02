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
        Mouse x: {{mouseX}}, Mouse y: {{mouseY}}<br>
        Touch x: {{touchX}}, Touch y: {{touchY}}
      </div>

      <canvas ref="board" width="375" height="600" @touchmove="touch" @touchstart="toggleTouchStart" @touchend="toggleTouchStart">
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

    const touchX = ref()
    const touchY = ref()
    const touchStart = ref(false)


    function toggleMouseIsDown(event) {
      event.type === 'mousedown' ? mouseIsDown.value = true : mouseIsDown.value = false
    }

    function toggleTouchStart(TouchEvent) {
      TouchEvent.type === 'touchstart' ? touchStart.value = true : touchStart.value = false
    }

    function clearBoard() {
      const ctx = board.value.getContext('2d')
      ctx.clearRect(0, 0, 800, 800)
    }

    function getMouseCoords(event) {
      mouseX.value = event.offsetX
      mouseY.value = event.offsetY
    }

    function getTouchCoords(TouchEvent) {
      const touch = TouchEvent.touches[0]
      touchX.value = touch.pageX
      touchY.value = touch.pageY
    }

    function draw(event) {
      getMouseCoords(event)
      const ctx = board.value.getContext('2d')
      let mx = event.offsetX
      let my = event.offsetY

      if(mouseIsDown.value) {
        ctx.beginPath()
        ctx.arc(mx, my, 10, 0 , 360 )
        ctx.fill()
      }
    }

    function touch(TouchEvent) {
      getTouchCoords(TouchEvent)
      const ctx = board.value.getContext('2d')
      const touch = TouchEvent.touches[0]
      const tx = touch.clientX
      const ty = touch.clientY

      if(touchStart.value) {
        console.log('touchstart')
        ctx.beginPath()
        ctx.arc(tx, ty, 10, 0, 360)
        ctx.fill()
      }
    }

    return {board, draw, clearBoard, toggleMouseIsDown, mouseIsDown, mouseX, mouseY, touchStart, touchX, touchY, toggleTouchStart, touch}
  }
}


</script>

<style scoped>

</style>
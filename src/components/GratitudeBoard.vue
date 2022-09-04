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

      <canvas ref="board" width="400" height="600" @touchmove="touch" @touchstart="toggleTouchStart" @touchend="toggleTouchStart"
      @mousemove="draw" @mousedown="toggleMouseIsDown" @mouseup="toggleMouseIsDown">
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
      ctx.clearRect(0, 0, window.innerWidth, window.innerHeight)
    }

    function drawDot(x, y, ctx) {
      ctx.beginPath()
      ctx.arc(x, y, Math.PI, 0, 360)
      ctx.fill()
    }

    function draw(event) {
      const ctx = board.value.getContext('2d')
      let mx = event.offsetX
      let my = event.offsetY

      if (mouseIsDown.value) {
        drawDot(mx, my, ctx)
      }
    }

    function touch(TouchEvent) {
      TouchEvent.preventDefault()
      TouchEvent.stopPropagation()

      const ctx = board.value.getContext('2d')
      const canvasPos = board.value.getBoundingClientRect()
      const touch = TouchEvent.touches[0]
      const tx = touch.clientX - canvasPos.x
      const ty = touch.clientY - canvasPos.y

      if (touchStart.value) {
        drawDot(tx, ty, ctx)
      }
    }

      return {
      board, mouseIsDown, mouseX, mouseY, touchStart, touchX, touchY,
        draw, clearBoard, toggleMouseIsDown, toggleTouchStart, touch,
      }
    }
  }


</script>

<style scoped>

</style>
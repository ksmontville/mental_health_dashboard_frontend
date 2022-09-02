<template>
  <div class="dashboard bg-wrapper bg-gradient">
  <nav>
    <DashboardNavbar />
  </nav>

  <div class="toolbar">
    <div class="container-fluid">
      <div class="input-group mb-3">
        <input type="file" class="form-control" id="imgUpload">
        <label class="input-group-text" for="imgUpload">Upload</label>
      </div>
    </div>
  </div>

    <button @click="drawRect">Draw Squares</button>
    <button @click="drawLine">Draw Lines</button>
    <canvas ref="board" width="300" height="400">
      This is a canvas
    </canvas>
  </div>
</template>

<script>
import {onMounted, onUpdated, ref} from "vue";

export default {
  name: "GratitudeBoard",

  setup() {

    const board = ref(null)

    onMounted(() => {

    })

    onUpdated(() => {

    })

    function drawRect() {
      const ctx = board.value.getContext('2d')
      ctx.fillStyle = 'rgb(200, 0, 0)'
      ctx.fillRect(10, 10, 100, 100)

      ctx.fillStyle = 'rgb(0, 200, 0, 0.5)'
      ctx.fillRect(50, 50, 100, 100)
    }

    function drawLine() {
      const ctx = board.value.getContext('2d')


      ctx.beginPath()
      ctx.strokeStyle = 'purple'
      ctx.moveTo(50, 50)
      ctx.lineTo(100, 100, )
      ctx.stroke()

      ctx.beginPath()
      ctx.strokeStyle = 'green'
      ctx.moveTo(500, 500)
      ctx.lineTo(-200, 200)
      ctx.stroke()

    }

    return {board, drawRect, drawLine}
  }
}

</script>

<style scoped>

</style>
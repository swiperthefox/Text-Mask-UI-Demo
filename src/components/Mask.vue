<template>
  <div class="mask-container">
    <div class="horizental-mask-controller mask-controller">
      <label>Start of mask:
      <input type="range" min="0" max="1000" v-model.number="start">
      </label>
      <label>Height of strip:
        <input type="range" min="0" max="1000" v-model.number="stripHeight">
      </label>
      <label>Gap between strips:
        <input type="range" min="0" max="1000" v-model.number="stripGap">
      </label>
      <label>Number of strips:
        <input type="range" min="0" max="20" step="1" v-model.number="strips">
      </label>
    </div>
    <svg id="mask">
      <rect v-for="i in strips" v-bind="config(i)" :key="i"></rect>
    </svg>
  </div>
</template>

<script>
export default {
  name: 'mask-v1',
  data: () => ({
    start: 250,
    stripHeight: 20,
    stripGap: 40,
    strips: 5
  }),
  props: [],
  methods: {
    config (i) {
      let x = '200'
      let y = Math.round((this.start + (i - 1) * (this.stripHeight + this.stripGap)) * 835 / 1000)
      let height = Math.round(this.stripHeight * 835 / 1000) + 'px'
      let width = '600'
      return { x, y, height, width }
    }
  }
}
</script>

<style>
.mask-container {
  position:absolute;
  top: 0px;
  left:0px;
  right: 0px;
  bottom: 0px;
}

#mask {
  width: 100%;
  height: 100%;
  top: 0px;
  left: 0px;
  position: absolute;
  z-index: 1000;
}
.mask-controller {
  z-index: 1002;
  width: 100%;
  position: relative;
}

.horizental-mask-controller input {
  width:80%;
  vertical-align: middle;
}

.horizental-mask-controller label {
  display: block;
  text-align: right;
}
input[type=range]::-moz-range-thumb {
  background-color: green;
}
rect {
  fill: rgba(200,200,200, 0.7)
}
</style>

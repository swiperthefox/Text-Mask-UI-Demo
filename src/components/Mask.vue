<template>
  <div class="mask-container">
    <div class="vertical-mask-controller mask-controller" v-if="vertical">
      <input type="range" min="0" max="1000" v-model.number="start">
      <input type="range" min="0" max="1000" v-model.number="vheight">
      <input type="range" min="0" max="1000" v-model.number="vgap">
      <input type="range" min="0" max="1000" :step="stripHeight + stripGap" v-model.number="vnum">
    </div>
    <div class="horizental-mask-controller mask-controller" v-else>
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
      <rect x="150" :y="startInPx + 'px'" height="1" width="650" style="fill: green"></rect>
      <rect x="120" :y="(startInPx + heightInPx) + 'px'" height="1" width="680" style="fill: green"></rect>
      <rect x="90" :y="(startInPx + heightInPx + gapInPx) + 'px'" height="1" width="710" style="fill: green"></rect>
      <rect x="60" :y="(startInPx + (strips-1)*(heightInPx + gapInPx)) + 'px'" height="1" width="740" style="fill: green"></rect>
    </svg>
  </div>
</template>

<script>
export default {
  name: 'MaskLayer',
  data: () => ({
    start: 250,
    stripHeight: 20,
    stripGap: 40,
    strips: 5,
    useVerticalControl: false
  }),
  props: ['vertical'],
  methods: {
    topOf (i) {
      return Math.round((this.start + (i - 1) * (this.stripHeight + this.stripGap)) * 835 / 1000)
    },
    config (i) {
      let x = '200'
      let y = this.topOf(i)
      let height = Math.round(this.stripHeight * 835 / 1000) + 'px'
      let width = '600'
      return { x, y, height, width }
    }
  },
  computed: {
    vheight: {
      get: function () {
        return this.start + this.stripHeight
      },
      set: function (v) {
        this.stripHeight = v - this.start
      }
    },
    vgap: {
      get: function () {
        return this.start + this.stripHeight + this.stripGap
      },
      set: function (v) {
        this.stripGap = v - this.start - this.stripHeight
      }
    },
    vnum: {
      get: function () {
        return this.start + (this.strips - 1) * (this.stripHeight + this.stripGap)
      },
      set: function (v) {
        v = Math.max(v, this.vgap)
        this.strips = Math.ceil((v - this.start) / (this.stripHeight + this.stripGap))
      }
    },
    startInPx: function () {
      return Math.round(this.start * 0.835)
    },
    heightInPx: function () {
      return Math.round(this.stripHeight * 0.835)
    },
    gapInPx: function () {
      return Math.round(this.stripGap * 0.835)
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
.vertical-mask-controller {
  z-index: 1002;
  position: absolute;
  transform: rotate(90deg);
  transform-origin: 80px  80px;
  /* we are hard coding the size of image here, since we want the rotated
   has the same height as the image. One possible way to avoid this hard
   coding is to use a hidden rotated img, and has this div has the same width
   as the rotated img. */
  width: 835px;
}
.vertical-mask-controller input {
  width: 100%;
  margin: 3px 0px;
}

rect {
  fill: rgba(200,200,200, 0.7)
}
</style>

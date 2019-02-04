<template>
  <div class="mask-container">
    <div class="vertical-mask-controller mask-controller">
      <input type="range" min="0" max="1000" v-model.number="firstBottomLine">
      <input type="range" min="0" max="1000" v-model.number="secondBottomLine">
      <input type="range" min="0" max="1000" v-model.number="stripTopEdge">
      <input type="range" min="0" max="1000" v-model.number="bottom">
    </div>

    <svg id="mask">
      <rect v-for="(strip, index) in stripConfigs" v-bind="strip" :key="index"></rect>
      <g>
        <rect x="150" :y="pixelOf(firstBottomLine) + 'px'" height="1" width="650"></rect>
        <rect x="120" :y="pixelOf(firstBottomLine + stripGap) + 'px'" height="1" width="680"></rect>
        <rect x="90" :y="pixelOf(firstBottomLine - stripHeight) + 'px'" height="1" width="710"></rect>
        <rect x="60" :y="pixelOf(bottom) + 'px'" height="1" width="740"></rect>
      </g>
    </svg>
  </div>
</template>
<script>
export default {
  name: 'MaskV3',
  data: () => ({
    firstBottomLine: 250,
    stripHeight: 20,
    stripGap: 60,
    num: 3
  }),
  props: [],
  computed: {
    stripConfigs: function () {
      let result = []
      for (let i = 0; i < this.num; ++i) {
        result.push({
          x: 200,
          y: this.pixelOf(this.firstBottomLine + i * this.stripGap - this.stripHeight),
          width: 600,
          height: this.pixelOf(this.stripHeight)
        })
      }
      return result
    },
    secondBottomLine: {
      get: function () {
        return this.firstBottomLine + this.stripGap
      },
      set: function (v) {
        this.stripGap = v - this.firstBottomLine
      }
    },
    stripTopEdge: {
      get: function () {
        return this.firstBottomLine - this.stripHeight
      },
      set: function (v) {
        this.stripHeight = this.firstBottomLine - v
      }
    },
    bottom: {
      get: function () {
        return this.firstBottomLine + (this.num - 1) * this.stripGap
      },
      set: function (v) {
        this.num = Math.round((v - this.firstBottomLine) / this.stripGap) + 1
      }
    }
  },
  methods: {
    pixelOf: function (v) {
      return Math.round(v * 0.835)
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
g rect {
    fill: green;
    z-index: 100;
}
</style>

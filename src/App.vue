<template>
  <div id="app">
    <h2>Make It Easier To Use</h2>
    <div>
    Try to adjust the parameters to mask all the lines English letters in the main text body. Then swtich the controller to vertical mode, do the same thing again.
    </div>
    <label>
      <input type="checkbox" v-model="useVerticalControl">
      Use Vertical controller
    </label>
    <div id="demo-content">
    <mask-layer :vertical="useVerticalControl"></mask-layer>
    <img src="./assets/sample.jpg" width="600" height="835">
    </div>
  </div>
</template>

<script>
import MaskLayer from './components/Mask'

export default {
  name: 'App',
  data: () => ({
    useVerticalControl: false
  }),
  components: {
    MaskLayer
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
#demo-content {
  position: relative;
}
img {
  display: block;
  margin-left: 200px;
}
</style>

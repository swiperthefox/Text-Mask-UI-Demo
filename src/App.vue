<template>
  <div id="app">
    <h2>Make It Easier To Use</h2>
    <div>
    <p>The folling image is a page of textbook of Chinese language. On each line of Chinese sentence,
    there is a line of "pinyin", which shows how to pronounce the corresponding Chinese character.
    Some time, it's desirable to cover these pronouncing hints.</p>
    <p>Try to adjust the parameters to cover all the lines of the main text body that is "pinyin" with gray strips.</p>
    <p>Then swtich the controller to vertical mode, do the same thing again.</p>
    <p>With the visual connections between slider thumbs and their effects, the job becomes much easier.</p>
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
  max-width: 900px;
}
#demo-content {
  position: relative;
  border: 1px solid gray;
  margin: 10px;
}
img {
  display: block;
  margin-left: 200px;
}
</style>

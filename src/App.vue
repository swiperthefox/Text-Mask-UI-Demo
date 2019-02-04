<template>
  <div id="app">
    <h2>Make It Easier To Use</h2>
    <div>
    <p>The folling image is a page of textbook of Chinese language. On each line of Chinese sentence,
    there is a line of "pinyin", which shows how to pronounce the corresponding Chinese character.
    Some time, it's desirable to cover these pronounciation hints.</p>
    <p>Try to adjust the parameters to cover all the lines of the main text body that is "pinyin" with gray strips.</p>
    <p>Then swtich the controller to vertical mode, do the same thing again.</p>
    <p>With the visual connections between slider thumbs and their effects, the job becomes much easier.</p>
    </div>
    <label>
      <input type="radio" v-model="maskName" value="mask-v1">
      <b>First version: </b> Choose four parameters to configurate the strips, and show the sliders for them.
    </label>
    <label>
      <input type="radio" v-model="maskName" value="mask-v2">
      <b>Second version: </b>By placing the slide bar vertically, we can provide visual connect between the knobs and their meaning.
    </label>
    <label>
      <input type="radio" v-model="maskName" value="mask-v3">
      <b>Third vesion: </b>Noticed that the most import thing is to put the bottom edge of the strips right above the texts that we want show. In version 2, the position of bottom edges depends on the value of three parameters. In this version, it only depends on two paramters. Now it's much easier to get it right.
    </label>
    <div id="demo-content">
    <component :is="maskName"></component>
    <img src="./assets/sample.jpg" width="600" height="835">
    </div>
  </div>
</template>

<script>
import MaskV1 from './components/Mask'
import MaskV2 from './components/MaskV2'
import MaskV3 from './components/MaskV3'

export default {
  name: 'App',
  data: () => ({
    maskName: 'mask-v1'
  }),
  components: {
    MaskV1,
    MaskV2,
    MaskV3
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
label {
  display: block;
}
</style>

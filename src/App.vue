<template>
  <div id="app">
    <vDrag>
      <itemDrag>1</itemDrag>
      <itemDrag>2</itemDrag>
      <itemDrag>3</itemDrag>
      <itemDrag>4</itemDrag>
      <itemDrag>5</itemDrag>
      <itemDrag>6</itemDrag>
      <itemDrag>7</itemDrag>
    </vDrag>
  </div>
</template>

<script>
import vDrag from './components/main.vue'
import itemDrag from './components/item-drag.vue'
export default {
  name: 'App',
  components: {
    vDrag,
    itemDrag
  }
}
</script>

<style>
html,body,#app {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}
</style>

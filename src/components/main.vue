<template>
  <div class="main-drag">
    <slot></slot>
  </div>
</template>
<style scoped>
  .main-drag {
    width: 100%;
    height: 100%;
    position: relative;
  }
</style>
<script>
  export default {
    name: 'v-drag',
    data () {
      return {}
    },
    methods: {
    }
  }
</script>

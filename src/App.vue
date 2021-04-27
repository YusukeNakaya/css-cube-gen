<template lang="pug">
.css-app
  h1.title CSS 3D CUBE
  CubeGen
</template>

<script>
import CubeGen from './components/CubeGen.vue'
import 'modern-css-reset'

export default {
  name: 'App',
  components: {
    CubeGen
  }
}
</script>

<style lang="scss">
@import url(https://fonts.googleapis.com/css2?family=Teko:wght@700&display=swap);

.css-app {
  font-family: 'Teko', sans-serif;

  .title {
    position: absolute;
    font-size: 100px;
    line-height: 1;
    color: rgba(100, 100, 100, 1);
  }
}
</style>

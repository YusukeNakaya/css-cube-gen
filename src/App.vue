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
@import url(https://fonts.googleapis.com/css2?family=Ubuntu:wght@300&display=swap);

.css-app {
  font-family: 'Ubuntu', sans-serif;
  background: #FEFEFE;

  .title {
    position: absolute;
    left: 25px;
    bottom: 20px;
    font-size: 50px;
    line-height: 1;
    color: rgba(200, 200, 200, 1);
  }
}
</style>

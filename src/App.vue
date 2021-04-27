<template lang="pug">
.css-app
  .info
    h1.title CSS 3D CUBE
    .link
      ul.list
        li.item
          a.anchor(href="https://github.com/YusukeNakaya/css-cube-gen" target="_blank")
            img.icon(src="./assets/github.svg" alt="GitHub")
        li.item
          a.anchor(href="https://twitter.com/s14garnet" target="_blank")
            img.icon(src="./assets/twitter.svg" alt="twitter")
        li.item
          a.anchor(href="https://codepen.io/YusukeNakaya" target="_blank")
            img.icon.-codepen(src="./assets/codepen.svg" alt="CodePen")
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

  .info {
    display: flex;
    align-items: center;
    position: absolute;
    z-index: 2;
    left: 25px;
    bottom: 20px;
  }

  .title {
    font-size: 50px;
    line-height: 1;
    color: rgba(200, 200, 200, 1);
  }

  .list {
    display: flex;
    list-style: none;
    margin: 0 0 0 30px;
    padding: 0;
  }

  .item {
    margin-right: 10px;
  }

  .icon {
    width: auto;
    height: 30px;

    &.-codepen {
      transform: scale(1.2);
    }
  }

  .anchor {
    display: block;
    opacity: 0.3;
    transition: 300ms;

    &:hover {
      opacity: 0.5;
      transform: translateY(-5px);
    }
  }
}
</style>

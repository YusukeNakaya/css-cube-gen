<template lang="pug">
.cube-gen
  .gen-form
    .width
      .label Width
      input.input(type="range" min="1" max="500" step="1" v-model="width")
    .height
      .label Height
      input.input(type="range" min="1" max="500" step="1" v-model="height")
    .depth
      .label Depth
      input.input(type="range" min="1" max="500" step="1" v-model="depth")
    .opacity
      .label Opacity
      input.input(type="range" min="0" max="1" step="0.01" v-model="opacity")
    .color
      .label Color #
      input.input(type="text" maxlength="6" v-model="color")
    .shadow
      .label Shadow
      input.input(type="number" v-model="shadowRatio")
  .gen-view
    .cube(:style="{transform: 'rotateX(' + rotateX + 'deg) rotateY(' + rotateY + 'deg)'}")
      .face.-face1(:style="{background: 'rgba(' + (red - 5 * shadowRatio) + ', ' + (green - 5 * shadowRatio) + ', ' + (blue - 5 * shadowRatio) + ', ' + opacity + ')', width: width + 'px', height: height + 'px', transform: 'translate(-50%, -50%) rotateY(0deg) translateZ(' + depth / 2 + 'px)'}")
      .face.-face2(:style="{background: 'rgba(' + (red - 10 * shadowRatio) + ', ' + (green - 10 * shadowRatio) + ', ' + (blue - 10 * shadowRatio) + ', ' + opacity + ')', width: depth + 'px', height: height + 'px', transform: 'translate(-50%, -50%) rotateY(90deg) translateZ(' + width / 2 + 'px)'}")
      .face.-face3(:style="{background: 'rgba(' + (red - 0 * shadowRatio) + ', ' + (green - 0 * shadowRatio) + ', ' + (blue - 0) + ', ' + opacity + ')', width: width + 'px', height: depth + 'px', transform: 'translate(-50%, -50%) rotateX(90deg) translateZ(' + height / 2 + 'px)'}")
      .face.-face4(:style="{background: 'rgba(' + (red - 20 * shadowRatio) + ', ' + (green - 20 * shadowRatio) + ', ' + (blue - 20 * shadowRatio) + ', ' + opacity + ')', width: width + 'px', height: depth + 'px', transform: 'translate(-50%, -50%) rotateX(-90deg) translateZ(' + height / 2 + 'px)'}")
      .face.-face5(:style="{background: 'rgba(' + (red - 10 * shadowRatio) + ', ' + (green - 10 * shadowRatio) + ', ' + (blue - 10 * shadowRatio) + ', ' + opacity + ')', width: depth + 'px', height: height + 'px', transform: 'translate(-50%, -50%) rotateY(-90deg) translateZ(' + width / 2 + 'px)'}")
      .face.-face6(:style="{background: 'rgba(' + (red - 15 * shadowRatio) + ', ' + (green - 15 * shadowRatio) + ', ' + (blue - 15 * shadowRatio) + ', ' + opacity + ')', width: width + 'px', height: height + 'px', transform: 'translate(-50%, -50%) rotateY(180deg) translateZ(' + depth / 2 + 'px)'}")
  .gen-code
    .html
      | Pug
      pre.pre
        code.code(@click="copy")
          | .your-cube
          |   .face.-face1
          |   .face.-face2
          |   .face.-face3
          |   .face.-face4
          |   .face.-face5
          |   .face.-face6
    .css
      | SCSS
      pre.pre
        code.code(@click="copy")
          | .your-cube {
          |   position: absolute;
          |   top: 50%;
          |   left: 50%;
          |
          |   .face {
          |     position: absolute;
          |
          |     &amp;.-face1 {
          |       width: {{width}}px;
          |       height: {{height}}px;
          |       transform: translate(-50%, -50%) rotateY(0deg) translateZ({{depth / 2}}px);
          |       background: rgba({{red - 5}}, {{green - 5}}, {{blue - 5}}, {{opacity}});
          |     }
          |
          |     &amp;.-face2 {
          |       width: {{depth}}px;
          |       height: {{height}}px;
          |       transform: translate(-50%, -50%) rotateY(90deg) translateZ({{width / 2}}px);
          |       background: rgba({{red - 10 * shadowRatio}}, {{green - 10 * shadowRatio}}, {{blue - 10 * shadowRatio}}, {{opacity}});
          |     }
          |
          |     &amp;.-face3 {
          |       width: {{width}}px;
          |       height: {{depth}}px;
          |       transform: translate(-50%, -50%) rotateX(90deg) translateZ({{height / 2}}px);
          |       background: rgba({{red}}, {{green}}, {{blue}}, {{opacity}});
          |     }
          |
          |     &amp;.-face4 {
          |       width: {{width}}px;
          |       height: {{depth}}px;
          |       transform: translate(-50%, -50%) rotateX(-90deg) translateZ({{height / 2}}px);
          |       background: rgba({{red - 20 * shadowRatio}}, {{green - 20 * shadowRatio}}, {{blue - 20 * shadowRatio}}, {{opacity}});
          |     }
          |
          |     &amp;.-face5 {
          |       width: {{depth}}px;
          |       height: {{height}}px;
          |       transform: translate(-50%, -50%) rotateY(-90deg) translateZ({{width / 2}}px);
          |       background: rgba({{red - 10 * shadowRatio}}, {{green - 10 * shadowRatio}}, {{blue - 10 * shadowRatio}}, {{opacity}});
          |     }
          |
          |     &amp;.-face6 {
          |       width: {{width}}px;
          |       height: {{height}}px;
          |       transform: translate(-50%, -50%) rotateY(180deg) translateZ({{depth / 2}}px);
          |       background: rgba({{red - 15 * shadowRatio}}, {{green - 15 * shadowRatio}}, {{blue - 15 * shadowRatio}}, {{opacity}});
          |     }
          |   }
          | }
</template>

<script>
export default {
  name: 'CubeGen',

  data () {
    return {
      width: 100,
      height: 100,
      depth: 100,
      opacity: 1,
      color: 'ff0000',
      rotateX: 0,
      rotateY: 0,
      shadowRatio: 2
    }
  },

  computed: {
    red () {
      return parseInt(this.color.substring(0,2), 16)
    },

    green () {
      return parseInt(this.color.substring(2,4), 16)
    },

    blue () {
      return parseInt(this.color.substring(4,6), 16)
    }
  },

  mounted () {
    window.addEventListener('mousemove', event => {
      this.rotateY = (event.clientX - window.innerWidth / 2) / 5
      this.rotateX = (event.clientY - window.innerHeight / 2) / 5 * -1
    })
  },

  methods: {
    copy (event) {
      const string = event.target.textContent
      navigator.clipboard.writeText(string)
      console.log(string)
    }
  }
}
</script>

<style scoped lang="scss">
.cube-gen {
  position: relative;
  perspective: 800px;
  width: 100%;
  height: 100vh;
}

.gen-form {
  position: absolute;
  top: 100px;
  left: 20px;

  .input {
    width: 200px;
  }
}

.gen-view {
  position: absolute;
  width: 100%;
  height: 100%;
  pointer-events: none;

  .cube {
    position: absolute;
    top: 50%;
    left: 50%;
    transform-style: preserve-3d;
  }

  .face {
    position: absolute;
    background: rgba(255, 0, 0, 0.2);

    &.-face1 {
      transform: rotateY(0deg) translateZ(50px);
    }

    &.-face2 {
      transform: rotateY(90deg) translateZ(50px);
    }

    &.-face3 {
      transform: rotateX(90deg) translateZ(50px);
    }

    &.-face4 {
      transform: rotateX(-90deg) translateZ(50px);
    }

    &.-face5 {
      transform: rotateY(-90deg) translateZ(50px);
    }

    &.-face6 {
      transform: rotateY(180deg) translateZ(50px);
    }
  }
}

.gen-code {
  position: absolute;
  top: 0;
  right: 20px;
  width: 400px;

  .pre {
    margin: 0;
    padding: 20px;
    background: rgba(0, 0, 0, 0.8);
    font-size: 10px;
    line-height: 1.2;
    color: #fff;
  }
}
</style>

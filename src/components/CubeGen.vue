<template lang="pug">
.cube-gen
  .gen-form
    .part.width
      .label Width
      input.input(type="range" min="1" max="500" step="1" v-model="width")
      input.subinput(type="number" v-model="width")
    .part.height
      .label Height
      input.input(type="range" min="1" max="500" step="1" v-model="height")
      input.subinput(type="number" v-model="height")
    .part.depth
      .label Depth
      input.input(type="range" min="1" max="500" step="1" v-model="depth")
      input.subinput(type="number" v-model="depth")
    .part.opacity
      .label Opacity
      input.input(type="range" min="0" max="1" step="0.01" v-model="opacity")
      input.subinput(type="number" v-model="opacity")
    .part.color
      .label Color #
      input.input(type="text" maxlength="6" v-model="color")
    .part.shadow
      .label Shadow
      input.input(type="number" v-model="shadowRatio")
    .part.class
      .label Class
      input.input(type="text" v-model="className")
      a.anchor(@click="updateClassName")
        img.icon(src="@/assets/reload.svg" alt="Reload")
  .gen-view
    .cube(:style="{transform: 'rotateX(' + rotateX + 'deg) rotateY(' + rotateY + 'deg)'}")
      .face.-front(:style="{background: 'rgba(' + (red - 5 * shadowRatio) + ', ' + (green - 5 * shadowRatio) + ', ' + (blue - 5 * shadowRatio) + ', ' + opacity + ')', width: width + 'px', height: height + 'px', transform: 'translate(-50%, -50%) rotateY(0deg) translateZ(' + depth / 2 + 'px)'}")
      .face.-left(:style="{background: 'rgba(' + (red - 10 * shadowRatio) + ', ' + (green - 10 * shadowRatio) + ', ' + (blue - 10 * shadowRatio) + ', ' + opacity + ')', width: depth + 'px', height: height + 'px', transform: 'translate(-50%, -50%) rotateY(90deg) translateZ(' + width / 2 + 'px)'}")
      .face.-top(:style="{background: 'rgba(' + (red - 0 * shadowRatio) + ', ' + (green - 0 * shadowRatio) + ', ' + (blue - 0) + ', ' + opacity + ')', width: width + 'px', height: depth + 'px', transform: 'translate(-50%, -50%) rotateX(90deg) translateZ(' + height / 2 + 'px)'}")
      .face.-bottom(:style="{background: 'rgba(' + (red - 20 * shadowRatio) + ', ' + (green - 20 * shadowRatio) + ', ' + (blue - 20 * shadowRatio) + ', ' + opacity + ')', width: width + 'px', height: depth + 'px', transform: 'translate(-50%, -50%) rotateX(-90deg) translateZ(' + height / 2 + 'px)'}")
      .face.-right(:style="{background: 'rgba(' + (red - 10 * shadowRatio) + ', ' + (green - 10 * shadowRatio) + ', ' + (blue - 10 * shadowRatio) + ', ' + opacity + ')', width: depth + 'px', height: height + 'px', transform: 'translate(-50%, -50%) rotateY(-90deg) translateZ(' + width / 2 + 'px)'}")
      .face.-back(:style="{background: 'rgba(' + (red - 15 * shadowRatio) + ', ' + (green - 15 * shadowRatio) + ', ' + (blue - 15 * shadowRatio) + ', ' + opacity + ')', width: width + 'px', height: height + 'px', transform: 'translate(-50%, -50%) rotateY(180deg) translateZ(' + depth / 2 + 'px)'}")
  .gen-code
    .html
      nav.nav
        ul.list
          li.item
            a.anchor(:class="{'-active' : mode.html === 'html'}" @click="mode.html = 'html'") HTML
          li.item
            a.anchor(:class="{'-active' : mode.html === 'pug'}" @click="mode.html = 'pug'") Pug
      pre.pre(@click="copy")
        code.code(v-if="mode.html === 'html'")
          | &lt;div class="{{className}}"&gt;
          |   &lt;div class="face -front"&gt;
          |   &lt;div class="face -left"&gt;
          |   &lt;div class="face -top"&gt;
          |   &lt;div class="face -bottom"&gt;
          |   &lt;div class="face -right"&gt;
          |   &lt;div class="face -back"&gt;
          | &lt;/div&gt;
        code.code(v-else-if="mode.html === 'pug'")
          | .{{className}}
          |   .face.-front
          |   .face.-left
          |   .face.-top
          |   .face.-bottom
          |   .face.-right
          |   .face.-back
    .css
      nav.nav
        ul.list
          li.item
            a.anchor(:class="{'-active' : mode.css === 'css'}" @click="mode.css = 'css'") CSS
          li.item
            a.anchor(:class="{'-active' : mode.css === 'scss'}" @click="mode.css = 'scss'") SCSS
      pre.pre(@click="copy")
        code.code(v-if="mode.css === 'css'")
          | .{{className}} {
          |   position: absolute;
          |   top: 50%;
          |   left: 50%;
          |   transform-style: preserve-3d;
          | }
          |
          | .{{className}} .face {
          |   position: absolute;
          | }
          |
          | .{{className}} .-front {
          |   width: {{width}}px;
          |   height: {{height}}px;
          |   transform: translate(-50%, -50%) rotateY(0deg) translateZ({{depth / 2}}px);
          |   background: rgba({{red - 5}}, {{green - 5}}, {{blue - 5}}, {{opacity}});
          | }
          |
          | .{{className}} .-left {
          |   width: {{depth}}px;
          |   height: {{height}}px;
          |   transform: translate(-50%, -50%) rotateY(90deg) translateZ({{width / 2}}px);
          |   background: rgba({{red - 10 * shadowRatio}}, {{green - 10 * shadowRatio}}, {{blue - 10 * shadowRatio}}, {{opacity}});
          | }
          |
          | .{{className}} .-top {
          |   width: {{width}}px;
          |   height: {{depth}}px;
          |   transform: translate(-50%, -50%) rotateX(90deg) translateZ({{height / 2}}px);
          |   background: rgba({{red}}, {{green}}, {{blue}}, {{opacity}});
          | }
          |
          | .{{className}} .-bottom {
          |   width: {{width}}px;
          |   height: {{depth}}px;
          |   transform: translate(-50%, -50%) rotateX(-90deg) translateZ({{height / 2}}px);
          |   background: rgba({{red - 20 * shadowRatio}}, {{green - 20 * shadowRatio}}, {{blue - 20 * shadowRatio}}, {{opacity}});
          | }
          |
          | .{{className}} .-right {
          |   width: {{depth}}px;
          |   height: {{height}}px;
          |   transform: translate(-50%, -50%) rotateY(-90deg) translateZ({{width / 2}}px);
          |   background: rgba({{red - 10 * shadowRatio}}, {{green - 10 * shadowRatio}}, {{blue - 10 * shadowRatio}}, {{opacity}});
          | }
          |
          | .{{className}} .-back {
          |   width: {{width}}px;
          |   height: {{height}}px;
          |   transform: translate(-50%, -50%) rotateY(180deg) translateZ({{depth / 2}}px);
          |   background: rgba({{red - 15 * shadowRatio}}, {{green - 15 * shadowRatio}}, {{blue - 15 * shadowRatio}}, {{opacity}});
          | }
        code.code(v-else-if="mode.css === 'scss'")
          | .{{className}} {
          |   $width: {{width}}px;
          |   $height: {{height}}px;
          |   $depth: {{depth}}px;
          |   $red: {{red}};
          |   $green: {{green}};
          |   $blue: {{blue}};
          |   $opacity: {{opacity}};
          |   $shadowRatio: {{shadowRatio}};
          |
          |   position: absolute;
          |   top: 50%;
          |   left: 50%;
          |   transform-style: preserve-3d;
          |
          |   .face {
          |     position: absolute;
          |
          |     &amp;.-front {
          |       width: $width;
          |       height: $height;
          |       transform: translate(-50%, -50%) rotateY(0deg) translateZ($depth / 2);
          |       background: rgba($red - 5 * $shadowRatio, $green - 5 * $shadowRatio, $blue - 5 * $shadowRatio, $opacity);
          |     }
          |
          |     &amp;.-left {
          |       width: $depth;
          |       height: $height;
          |       transform: translate(-50%, -50%) rotateY(90deg) translateZ($width / 2);
          |       background: rgba($red - 10 * $shadowRatio, $green - 10 * $shadowRatio, $blue - 10 * $shadowRatio, $opacity);
          |     }
          |
          |     &amp;.-top {
          |       width: $width;
          |       height: $depth;
          |       transform: translate(-50%, -50%) rotateX(90deg) translateZ($height / 2);
          |       background: rgba($red, $green, $blue, $opacity);
          |     }
          |
          |     &amp;.-bottom {
          |       width: $width;
          |       height: $depth;
          |       transform: translate(-50%, -50%) rotateX(-90deg) translateZ($height / 2);
          |       background: rgba($red - 20 * $shadowRatio, $green - 20 * $shadowRatio, $blue - 20 * $shadowRatio, $opacity);
          |     }
          |
          |     &amp;.-right {
          |       width: $depth;
          |       height: $height;
          |       transform: translate(-50%, -50%) rotateY(-90deg) translateZ($width / 2);
          |       background: rgba($red - 10 * $shadowRatio, $green - 10 * $shadowRatio, $blue - 10 * $shadowRatio, $opacity);
          |     }
          |
          |     &amp;.-back {
          |       width: $width;
          |       height: $height;
          |       transform: translate(-50%, -50%) rotateY(180deg) translateZ($depth / 2);
          |       background: rgba($red - 15 * $shadowRatio, $green - 15 * $shadowRatio, $blue - 15 * $shadowRatio, $opacity);
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
      color: '6C99C6',
      rotateX: 0,
      rotateY: 0,
      shadowRatio: 2,
      className: Math.random().toString(32).substring(2),
      mode: {
        css: 'css',
        html: 'html'
      }
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
    },

    updateClassName () {
      this.className = Math.random().toString(32).substring(2)
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
  top: 20px;
  left: 20px;

  .anchor {
    display: block;
    margin-left: 10px;
    transition: 300ms;
    cursor: pointer;

    &:hover {
      transform: rotateZ(-90deg);
      opacity: 0.7;
    }
  }

  .icon {
    width: 20px;
    height: auto;
  }

  .input {
    width: 200px;
  }

  .subinput {
    width: 70px;
    margin-left: 30px;
    text-align: right;
  }

  .part {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }

  .label {
    width: 80px;
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

    &.-front {
      transform: rotateY(0deg) translateZ(50px);
    }

    &.-left {
      transform: rotateY(90deg) translateZ(50px);
    }

    &.-top {
      transform: rotateX(90deg) translateZ(50px);
    }

    &.-bottom {
      transform: rotateX(-90deg) translateZ(50px);
    }

    &.-right {
      transform: rotateY(-90deg) translateZ(50px);
    }

    &.-back {
      transform: rotateY(180deg) translateZ(50px);
    }
  }
}

.gen-code {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 450px;

  .list {
    display: flex;
    margin: 0;
    padding: 0;
    list-style: none;
  }

  .item {
    position: relative;

    &:not(:first-child) {
      margin-left: 14px;
      padding-left: 15px;

      &::before {
        content: '';
        position: absolute;
        top: calc(50% - 7px);
        left: 0;
        width: 1px;
        height: 14px;
        background: #999;
      }
    }
  }

  .anchor {
    cursor: pointer;
    opacity: 0.3;
    transition: 300ms;

    &.-active {
      opacity: 1;
    }
  }

  .pre {
    display: block;
    margin: 10px 0 0 0;
    padding: 15px;
    background: rgba(0, 0, 0, 0.8);
    font-size: 10px;
    line-height: 1.2;
    color: #fefefe;
    border-radius: 5px;
    cursor: pointer;

    &:active {
      opacity: 0.9;
    }
  }

  .css {
    margin-top: 20px;
  }
}
</style>

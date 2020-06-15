<template>
  <div class="cont">
    <div class="cover-text" :style="{animationName: anim, animationDuration: duration +'ms'}"></div>
    <div class="show" :style="{opacity: opacity}">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "TextReveal",
  props: {
    text: String,
    duration: {
      type: Number,
      default: 700
    },
    delay: {
      type: Number,
      default: 300
    }
  },
  data() {
    return {
      textT: "",
      anim: "",
      opacity: "",
      tag: "",
      reveal: false
    };
  },
  mounted() {
    let text = this.$slots.default[0].children[0].text;
    let len = text.length;
    this.tag = this.$slots.default[0].tag;
    for (let i = 0; i < len; i++) {
      this.textT += " ";
    }
    setTimeout(() => {
      this.anim = "text-reveal";
      setTimeout(() => {
        this.opacity = 1;
        this.reveal = true;
        this.textT = text;
      }, this.duration * 0.3);
    }, this.delay);
  }
};
</script>

<style>
.show {
  opacity: 0;
  transition: opacity 0.3s;
  display: inline-block;
}
.text-line {
  word-wrap: break-word;
}
.cont {
  position: relative;
  display: inline-block;
  overflow: hidden;
  width: auto;
  height: auto;
}
.cover-text {
  position: absolute;
  background-color: var(--accent);
  display: inline-block;
  height: 100%;
  width: 100%;
  transform: translateX(102%);
  z-index: 10;
}

@keyframes text-reveal {
  0% {
    transform: translateX(-100%);
  }

  100% {
    transform: translateX(110%);
  }
}
</style>


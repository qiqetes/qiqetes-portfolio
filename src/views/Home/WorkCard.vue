<template>
  <div>
    <div class="work-card" :style="{ opacity: transparency }">
      <h4>{{ work.name }}</h4>
      <p style="white-space: pre-line">{{ work.description }}</p>
      <div class="row" style="margin: auto">
        <div class="col-6 col-lg-7" style="padding: 0">
          <div class="row justify-content-start">
            <ul style="margin: 12px">
              <li
                v-for="tag in work.tags"
                :key="work.name + tag"
                :class="tag != highlightedTag ? 'tag' : 'tag highlight'"
                v-on:click="onClickTag(tag)"
              >
                {{ tag }}
              </li>
            </ul>
          </div>
        </div>
        <div class="col-6 col-lg-5 align-self-end" style="padding: 0">
          <!-- TODO: add a view live link -->
          <div class="row justify-content-end">
            <button v-if="work.live" v-on:click="goToLink(work.live)">
              live
              <i class="fas fa-play"></i>
            </button>
            <button v-if="work.link" v-on:click="goToLink(work.link)">
              source
              <i class="fas fa-code"></i>
            </button>
            <button v-if="!work.link" disabled>
              no source
              <i class="fas fa-code"></i>
            </button>
            <button
              v-if="work.demo"
              style="cursor: none"
              @mouseenter="onMouseMove($event)"
              @mouseleave="hoveredDemo = false"
            >
              demo
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="demo" v-if="hoveredDemo" :style="{ left: left + 'px', top: top + 'px' }">
      <img :src="demoImg" alt=""/>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      transparency: 0,
      yIndex: 0,
      actual: 0,
      cT: this.changeTransparency,
      hoveredDemo: false,
      demoImg: "",
      left: 0,
      top: 0,
    };
  },
  created() {
    window.addEventListener("scroll", this.changeTransparency);
  },
  mounted() {
    this.yIndex = this.$el.getBoundingClientRect().top - window.innerHeight;
    this.changeTransparency;
    if (this.work.demo) {
      this.demoImg = require("@/assets/" + this.work.demo);
    }
  },
  props: {
    work: Object,
    onClickTag: Function,
    highlightedTag: String,
  },
  methods: {
    goToLink(link) {
      console.log("Redirecting to: " + link);
      window.open(link);
    },
    changeTransparency() {
      //  TODO: rename this method to eventHandler
      if (window.scrollY - 50 > this.yIndex && this.transparency != 1) {
        this.transparency = 1;
      } // FIXME: with enter it will behave better
    },
    onMouseMove(e) {
      this.hoveredDemo = true
      this.left = e.pageX;
      this.top = e.screenY;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../assets/scss/mixins.scss";

.work-card {
  font-family: "Space Mono";
  li {
    display: inline-block;
    margin: 5px;
  }
  ul {
    padding-left: 0;
  }
  padding: 25px;
  border-radius: 30px;
  @include box-shadow(2);
  transition: opacity 1s;
  margin-bottom: 15px;
  background-color: var(--q-sec);
}

.tag {
  font-size: 1em;
  padding: 2px;
  border-radius: 20px;
  padding: 2px 10px 2px 10px;
  color: var(--q-sec);
  background-color: var(--q-tag);
  white-space: nowrap;
  cursor: pointer;
}
.highlight {
  animation: color-pulse 2s ease-in infinite;
}

@keyframes color-pulse {
  0% {
    background-color: var(--accent2);
  }
  50% {
    background-color: var(--q-tag);
  }
  100% {
    background-color: var(--accent2);
  }
}
button {
  padding: 4px 12px 4px 12px;
  margin: 5px;
  i {
    margin-left: 0;
  }
}
h4 {
  font-weight: 900;
}
.demo {
  position: fixed;
  z-index: 99;
  max-width: 100vw;
}
</style>

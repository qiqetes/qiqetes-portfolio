<template>
  <div id="app">
    <Home />
    <Work />
    <Skills />
    <!-- scroll item -->
    <transition name="fade">
      <div class="scroll-down row justify-content-center" v-if="scrollVisible">
        <div>
          <div class="row justify-content-center">scroll</div>
          <div class="row justify-content-center">
            <i class="fa fa-chevron-down"></i>
          </div>
        </div>
      </div>
    </transition>

    <!-- Theme switch button -->
    <transition name="fade">
      <div class="night-mode" v-on:click="switchTheme()" v-if="scrollVisible">
        <i class="fas fa-moon" v-if="nightMode"></i>
        <i class="far fa-moon" v-if="!nightMode"></i>
      </div>
    </transition>

    <!-- particles -->
    <div class="particles" :style="{top: parallaxOffset+'px'}">
      <div id="particles-js"></div>
    </div>
  </div>
</template>

<script>
import "./assets/particles.min.js";
import Home from "./views/Home/Home";
import Work from "./views/Work/Work";
import Skills from "./views/Skills/Skills";

export default {
  mounted() {
    this.initParticles();
    window.addEventListener("scroll", this.scrollHandler);
  },
  components: {
    Home,
    Work,
    Skills
  },
  data() {
    return {
      parallaxOffset: 0,
      changingWord: "...",
      scrollVisible: true,
      nightMode: false
    };
  },
  methods: {
    initParticles() {
      window.particlesJS("particles-js", {
        particles: {
          number: {
            value: 80,
            density: {
              enable: false,
              value_area: 700
            }
          },
          color: {
            value: "#444455"
          },
          opacity: {
            value: 0.5,
            random: true,
            anim: {
              enable: true,
              speed: 0.2,
              opacity_min: 0.1,
              sync: false
            }
          },
          size: {
            value: 3,
            random: true,
            anim: {
              enable: false,
              speed: 20,
              size_min: 0.1,
              sync: false
            }
          },
          line_linked: {
            enable: false
          },
          move: {
            enable: true,
            speed: 1,
            direction: "none",
            random: true,
            straight: false,
            out_mode: "out",
            bounce: false,
            attract: {
              enable: false,
              rotateX: 600,
              rotateY: 1200
            }
          }
        },
        interactivity: {
          detect_on: "canvas",
          events: {
            onhover: {
              enable: false,
              mode: "grab"
            },
            onclick: {
              enable: false,
              mode: "push"
            },
            resize: true
          }
        },
        retina_detect: true
      });
    },
    scrollHandler() {
      let y = window.scrollY;
      if (y > 25) this.scrollVisible = false;
      else this.scrollVisible = true;
      this.parallaxOffset = y * 0.5;
    },
    switchTheme() {
      this.nightMode = !this.nightMode;
      let el = document.getElementsByTagName("BODY")[0];
      console.log(el);
      if (this.nightMode == true) {
        el.setAttribute("data-theme", "dark");
      } else {
        el.setAttribute("data-theme", "light");
      }
    }
  }
};
</script>


<style lang="scss">
@import "./assets/scss/mixins.scss";

body {
  --q-bg: rgb(252, 252, 252);
  --q-sec: white;
  --primary: #2c3e50;
  --q-tag: rgb(53, 53, 53);
}
body[data-theme="dark"] {
  // TODO: fucking ugly colors
  --q-bg: #2d2a2e;
  --q-sec: #2d2a2d;
  --primary: rgb(252, 252, 252);
  --q-tag: rgb(219, 219, 219);
}
.card {
  background-color: transparent !important;
}

html {
  h1 {
    -webkit-user-select: none;
    font-family: "Space Mono", monospace;
    font-size: 3.2em;
    padding: 0;
    margin: 0;
  }
  h2 {
    font-family: "Questrial", sans-serif;
    font-size: 1.8em;
  }
  h5 {
    margin-top: 30px;
  }

  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  width: 100%;
  height: 100vh;
}
.app-container {
  padding-left: 20px;
  padding-right: 20px;
  height: 200px;
  box-sizing: border-box;
}

body {
  font-family: "Space Mono", sans-serif;
  margin: 0px;
  padding: 0px;
  height: 3000px;
  display: block;
  overflow: hidden;
  overflow-y: auto;
  color: var(--primary);
  background-color: var(--q-bg);
  ul {
    list-style: none;
    padding-left: 0;
  }
}
body::-webkit-scrollbar {
  width: 0.5em;
}
body::-webkit-scrollbar-track {
  background-color: rgb(230, 230, 230);
}

body::-webkit-scrollbar-thumb {
  background-color: var(--primary);
  // outline: 1px solid slategrey;
}

.particles {
  position: absolute;
  z-index: -20;
  top: 0;
  width: 100%;
  height: 100vh;
  #particles-js {
    width: 100%;
    height: 100%;
  }
}

button {
  margin: 12px;
  padding: 15px 25px 15px 25px;
  font-family: "Space Mono";
  background-color: var(--q-sec);
  border: 0;
  border-radius: 100px;

  @include box-shadow(2);
  color: var(--primary);
  transition: box-shadow 0.5s;

  h2 {
    margin: 0;
  }
}

button:focus {
  outline: 1px solid transparent;
  outline-offset: -4px;
}
button:hover {
  @include box-shadow(3);
}

button:active {
  transform: scale(0.99);
}
button:disabled {
  box-shadow: none;
  border: 2px solid var(--primary);
  border-radius: 25px;
}
i {
  margin-left: 10px;
}

// scroll item
.scroll-down {
  width: 100% !important;
  position: absolute;
  bottom: 20px;
  animation: pulse 2s;
  animation-iteration-count: infinite;
  animation-timing-function: ease;
  transition: opacity 1s;
}
.fade-leave-active {
  animation: fade 1s;
}
@keyframes fade {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
@keyframes pulse {
  0% {
    transform: translateY(0);
  }
  15% {
    transform: translateY(-15px);
  }
  30% {
    transform: translateY(0px);
  }
  100% {
    transform: translateY(0);
  }
}

@keyframes btn-reveal {
  0% {
    transform: translateY(-140%);
    @include box-shadow(2);
  }
  100% {
    transform: translateY(0%);
  }
}

.night-mode {
  position: absolute;
  left: 40px;
  bottom: 40px;
}
</style>

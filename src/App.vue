<template>
  <div id="app">
    <MyNav :solid="turnSolidNav"></MyNav>
    <router-view></router-view>

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

    <!-- Theme switch button-->
    <transition name="fade">
      <div class="night-mode column container" v-if="scrollVisible">
        <div class="row justify-content-center night-text">{{themeName}}</div>
        <br />
        <br />
        <br />
        <div class="row justify-content-center" v-on:click="switchTheme()">
          <i class="fas fa-moon" v-if="nightMode"></i>
          <i class="far fa-moon" v-if="!nightMode"></i>
        </div>
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
import MyNav from "./components/MyNav";
import TextReveal from "./components/TextReveal";

export default {
  components: {
    MyNav,
    TextReveal
  },

  mounted() {
    this.initParticles();
    window.addEventListener("scroll", this.scrollHandler);
    this.logoY = document.getElementById("logo").getBoundingClientRect().top;
  },
  created() {
    let cookie = this.getCookie("theme");
    if (cookie) {
      if (cookie == "dark") {
        this.switchTheme();
      }
    } else {
      const userPrefersDark =
        window.matchMedia &&
        window.matchMedia("(prefers-color-scheme: dark)").matches;
      if (userPrefersDark) this.switchTheme();
    }
  },
  data() {
    return {
      parallaxOffset: 0,
      changingWord: "...",
      scrollVisible: true,
      nightMode: false,
      turnSolidNav: false,
      logoY: 0,
      themeName: "CHANGE THEME"
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
      if (y > 25) {
        this.scrollVisible = false;
        if (y > this.logoY) {
          this.turnSolidNav = true;
        } else {
          this.turnSolidNav = false;
        }
      } else this.scrollVisible = true;
      this.parallaxOffset = y * 0.5;
    },
    switchTheme() {
      this.nightMode = !this.nightMode;
      let el = document.getElementsByTagName("BODY")[0];
      if (this.nightMode == true) {
        el.setAttribute("data-theme", "dark");
        this.setCookie("theme", "dark");
        this.themeName = "LIGHT MODE";
      } else {
        el.setAttribute("data-theme", "light");
        this.setCookie("theme", "light");
        this.themeName = "DARK MODE";
      }
    },
    setCookie(key, value) {
      var expires = new Date();
      expires.setTime(expires.getTime() + 1 * 24 * 60 * 60 * 1000);
      document.cookie = key + "=" + value + ";expires=" + expires.toUTCString();
    },
    getCookie(key) {
      var keyValue = document.cookie.match("(^|;) ?" + key + "=([^;]*)(;|$)");
      return keyValue ? keyValue[2] : null;
    }
  }
};
</script>


<style lang="scss">
@import "./assets/scss/mixins.scss";

body {
  --q-bg: rgb(252, 252, 252);
  --q-scroll-bg: rgb(230, 230, 230);
  --q-sec: white;
  --primary: #2c3e50;
  --accent: #a04f64;
  --accent2: #bd687e;
  --q-tag: rgb(53, 53, 53);
}
body[data-theme="dark"] {
  // TODO: fucking ugly colors
  --q-bg: #1c1c1e;
  --q-sec: #2d2a2d;
  --q-scroll-bg: #221f22;
  --accent: #2bf0ab;
  --accent2: #d0f5e8;
  --primary: rgb(252, 252, 252);
  --q-tag: #2bf0ab;
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
  background-color: var(--q-scroll-bg);
}

body::-webkit-scrollbar-thumb {
  background-color: var(--accent);
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
  font-family: "Space Mono" !important;
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
@keyframes pulse-opacity {
  0% {
    opacity: 0;
  }
  20% {
    opacity: 1;
  }
  30% {
    opacity: 0;
  }
  100% {
    opacity: 0;
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
  position: fixed;

  padding: 0 !important;
  width: 20px;
  left: 40px;
  bottom: 40px;
  .night-text {
    animation: pulse-opacity 5s ease-in infinite;
    transform: rotate(90deg);
    @media (max-width: 768px) {
      display: none;
    }
  }
  div {
    white-space: nowrap;
    i {
      cursor: pointer;
      margin: 0;
    }
  }
}

h1 {
  font-family: "Questrial" !important;
  span {
    color: var(--accent);
    font-family: "Space Mono", monospace;
    font-size: 0.8em;
  }
}

a {
  color: inherit;
}
a:link {
  text-decoration: none;
}
a:hover {
  color: inherit;
}
</style>

<template>
  <div id="app">
    <Home />
    <Work />

    <div class="particles" :style="{top: parallaxOffset+'px'}">
      <div id="particles-js"></div>
    </div>
  </div>
</template>

<script>
import "./assets/particles.min.js";
import Home from "./views/Home/Home.vue";
import Work from "./views/Work/Work";

export default {
  mounted() {
    window.scrollTo(0, 0);
    this.initParticles();
  },
  components: {
    Home,
    Work
  },
  data() {
    return {
      parallaxOffset: 0,
      changingWord: "..."
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
    }
  }
};
</script>


<style lang="scss">
html {
  h1 {
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
  font-family: "Questrial", sans-serif;
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
  font-family: "Questrial", sans-serif;
  margin: 0px;
  padding: 0px;
  height: 10000px;
  display: block;
  overflow: hidden;
  overflow-y: auto;
  color: #2c3e50;

  ul {
    list-style: none;
  }
}
body::-webkit-scrollbar {
  width: 0.5em;
}
body::-webkit-scrollbar-track {
  background-color: rgb(230, 230, 230);
}

body::-webkit-scrollbar-thumb {
  background-color: #2c3e50;
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
</style>

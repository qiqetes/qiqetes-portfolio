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
@mixin box-shadow($level) {
  @if $level == 1 {
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  } @else if $level == 2 {
    box-shadow: 0px 6px 20px rgba(0, 0, 0, 0.2);
  } @else if $level == 3 {
    box-shadow: 0px 10px 40px rgba(0, 0, 0, 0.3);
  } @else if $level == 4 {
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 40px rgba(0, 0, 0, 0.1);
  } @else if $level == 5 {
    box-shadow: 0 19px 38px rgba(0, 0, 0, 0.3), 0 15px 12px rgba(0, 0, 0, 0.22);
  }
}

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
  height: 3000px;
  display: block;
  overflow: hidden;
  overflow-y: auto;
  color: #2c3e50;
  background-color: rgb(253, 253, 253);
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

button {
  margin: 12px;
  padding: 15px 25px 15px 25px;
  font-family: "Space Mono";
  background-color: white;
  border: 0;
  border-radius: 100px;

  @include box-shadow(2);
  color: #2c3e50;
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
  border: 2px solid #2c3e50;
  border-radius: 25px;
}
i {
  margin-left: 10px;
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
</style>

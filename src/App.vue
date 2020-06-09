<template>
  <div id="app">
    <div class="container my-cont">
      <div class="row justify-content-center align-items-end logo-cont">
        <TextReveal :duration="1000">
          <h1>qiqetes.</h1>
        </TextReveal>
      </div>
      <div class="row justify-content-center">
        <TextReveal :duration="700" :delay="1000">
          <h5
            style="text-align:center; line-height: 30px; display:inline-block;"
          >Greetings, I'm Enric Llopis and I'm a Computer Science student who develops...</h5>
        </TextReveal>
      </div>
      <div class="row justify-content-center">
        <div class="col-md-12 col-lg-6">
          <div class="row justify-content-center">
            <div class="col-md-auto">
              <div class="row justify-content-center">
                <MyButton i="fab fa-github-alt" :onClick="openGitHub">Github</MyButton>
              </div>
            </div>
            <div class="col-md-auto">
              <div class="row justify-content-center">
                <MyButton :onClick="goToWorkSection">Work</MyButton>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- TODO: change it to a different component -->
    <div class="particles" :style="{top: parallaxOffset+'px'}">
      <div id="particles-js"></div>
    </div>
  </div>
</template>

<script>
import "./assets/particles.min.js";
import TextReveal from "./components/TextReveal";
import MyButton from "./components/MyButton.vue";

export default {
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },

  mounted() {
    window.scrollTo(0, 0);
    this.initParticles();
  },
  data() {
    return {
      parallaxOffset: 0
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

    handleScroll() {
      let t = window.scrollY;
      this._data.parallaxOffset = t * 0.5;
    },
    openGitHub() {
      window.open("https://github.com/qiqetes");
    },
    goToWorkSection() {
      let y = document.getElementById("app").scrollHeight;
      window.scroll({ left: 0, top: y, behavior: "smooth" });
    }
  },
  components: {
    TextReveal,
    MyButton
  }
};
</script>
<style lang="scss">
#app {
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

  color: #2c3e50;
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
  // font-family: 'Questrial', sans-serif;
  margin: 8px;
  padding: 0px;
  height: 10000px;
  display: block;
  overflow: hidden;
  overflow-y: auto;

  // ul {
  //   list-style: none;
  // }
}

.my-cont {
  height: 100%;
}
.logo-cont {
  height: 40%;
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

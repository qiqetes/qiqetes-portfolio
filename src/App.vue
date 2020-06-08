<template>
  <div id="app">
    <div class="logo">
      <TextReveal :duration="1000">
        <h1>qiqetes.</h1>
      </TextReveal>
    </div>
    <div class="center-content" style="top:45% ">
    
      <TextReveal :duration="700" :delay="1000">
        <div
          style="text-align:center; margin-top:8px; line-height: 20px; display:inline-block;"
        >Greetings, I'm Enric Llopis and I'm a Computer Science student who develops...</div>
      </TextReveal>
      <div>
        <MyButton i="fab fa-github-alt" :onClick="openGitHub">Github</MyButton>
        <MyButton :onClick="goToWorkSection">Work</MyButton>
      </div>
    </div>

    <div class="particles">
      <div id="particles-js"></div>
    </div>
  </div>
</template>
<script>
import "./assets/particles.min.js";
import TextReveal from "./components/TextReveal";
import MyButton from "./components/MyButton.vue";

export default {
  mounted() {
    window.scrollTo(0, 0);
    this.initParticles();
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
    openGitHub() {
      window.open("https://github.com/qiqetes");
    },
    goToWorkSection() {
      let y = document.getElementById("app").scrollHeight;
      console.log(y);
      window.scroll(0, y);
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

.center-content {
  position: absolute;
  min-width: 80%;
  left: 50%;
  transform: translate(-50%, 0);
  text-align: center;
}

.logo {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  h1 {
    font-size: 3em;
    padding: 0;
    margin: 0;
  }
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

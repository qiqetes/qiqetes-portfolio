<template>
  <div class="home">
    <MyNav :solid="turnSolidNav" />
    <div class="container my-cont">
      <div class="row justify-content-center align-items-end logo-cont">
        <TextReveal :duration="1000">
          <h1 id="logo">{{name}}</h1>
        </TextReveal>
      </div>
      <div class="row justify-content-center">
        <div class="col-9">
          <div class="row justify-content-center">
            <TextReveal :duration="700" :delay="1000">
              <h5
                style="text-align:center; line-height: 30px; display:inline-block;"
              >{{greetingMsg}}{{changingWord}}</h5>
            </TextReveal>
          </div>
        </div>
      </div>
      <div class="row justify-content-center">
        <div class="col-md-12 col-lg-6">
          <div class="row justify-content-center">
            <div class="col-md-auto">
              <div class="row justify-content-center">
                <Button v-on:click="openGitHub">
                  <h2>
                    Github
                    <i class="fab fa-github-alt"></i>
                  </h2>
                </Button>
              </div>
            </div>
            <div class="col-md-auto">
              <div class="row justify-content-center">
                <button v-on:click="goToWorkSection">
                  <h2>Work</h2>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TextReveal from "../../components/TextReveal";

import MyNav from "./MyNav";

export default {
  data() {
    return {
      parallaxOffset: 0, // Don't change
      changingWord: "...", // Don't change
      turnSolidNav: false, // Changes the transparency of the navBar
      logoY: 0, // logo Y coordinate
      greetingMsg:
        "Greetings, I'm Enric Llopis and I'm a Computer Science student who develops",
      name: "qiqetes.",
      githubPath: "https://github.com/qiqetes"
    };
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
  mounted() {
    this.logoY = document.getElementById("logo").getBoundingClientRect().top;
  },
  methods: {
    handleScroll() {
      let t = window.scrollY;
      if (t > this.logoY) this.turnSolidNav = true;
      else this.turnSolidNav = false;
      this._data.parallaxOffset = t * 0.5;
    },
    changeWord() {
      let words = [
        "web pages",
        "videogames",
        "android apps",
        "anything really"
      ];
      let i = 0;
      setInterval(() => {
        i += 1;
        i = i % words.length;
        this.morphWord(words[i % words.length]);
      }, 5000);
    },
    morphWord(word) {
      let aux = this.changingWord;
      let maxL = aux.length;
      if (word.length > aux) aux = word.length;
    },
    openGitHub() {
      window.open(this.githubPath);
    },
    goToWorkSection() {
      let y = document.getElementById("app").getBoundingClientRect().bottom;
      y -= 40; // The Nav var height
      window.scroll({ left: 0, top: y, behavior: "smooth" });
    }
  },
  components: {
    TextReveal,
    MyNav
  }
};
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  height: 100%;
}
.my-cont {
  height: 100%;
}
.logo-cont {
  height: 40%;
}
</style>

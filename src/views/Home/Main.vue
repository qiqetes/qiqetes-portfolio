<template>
  <div class="container my-cont">
    <div class="row justify-content-center align-items-end logo-cont">
      <TextReveal :duration="1000">
        <h1 id="logo">{{name}}</h1>
      </TextReveal>
    </div>
    <div class="row justify-content-center">
      <div class="col-10">
        <div class="small-about row justify-content-center">
          <TextReveal :duration="700" :delay="1000">
            <p style="font-family: 'Questrial', sans-serif">
              <span style="font-weight: 700">{{greetingMsg}}</span>
              {{about}}
            </p>
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
</template>

<script>
import TextReveal from "../../components/TextReveal";

export default {
  data() {
    return {
      parallaxOffset: 0, // Don't change
      changingWord: "...", // Don't change
      turnSolidNav: false, // Changes the transparency of the navBar
      logoY: 0, // logo Y coordinate
      //
      //
      // TODO: maybe this should be in the json with all the info
      greetingMsg: "Hi, my name is Enric Llopis 👨‍💻. ",
      about:
        "I'm a Computer Science student based in Valencia, Spain specializing in building and designing cool websites and applications. But not only that, I have a great passion for Data analysis 📈 and Game Development 👾.",
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
      let y = document.getElementById("work").offsetTop;
      y -= 40; // The Nav var height
      window.scroll({ left: 0, top: y, behavior: "smooth" });
    }
  },
  components: {
    TextReveal
  }
};
</script>

<style lang="scss">
#logo {
  font-family: "Space Mono", monospace !important;
}
.home {
  width: 100%;
  height: 100%;
}
.my-cont {
  height: 100%;
  p {
    font-size: 1.3em;
    color: var(--primary) !important;
  }
}
.small-about {
  margin-top: 28px;
}
.logo-cont {
  height: 40%;
}
@media (max-width: 576px) {
  .logo-cont {
    height: 20%;
  }
}
h2 {
  font-family: "Space Mono";
  font-weight: 900;
}
button {
  h2 {
    font-family: "Space Mono", monospace;
  }
}
</style>
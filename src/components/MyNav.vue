<template>
  <!-- TODO: DROPDOWN MENU FOR SM SCREENS -->
  <nav :class="{solid: solid}">
    <ul class="nav justify-content-end">
      <transition name="fade">
        <li class="mr-auto" v-if="solid">
          <h3 v-on:click="goTop()">qiqetes.</h3>
        </li>
      </transition>
      <li class="nav-item align-self-center">Blog</li>
      <li class="nav-item align-self-center">
        <a :href="resumeLink">Resume</a>
      </li>
      <li class="nav-item align-self-center">About me</li>
    </ul>
  </nav>
</template>

<script>
import dataJson from "../assets/work.json";

export default {
  data() {
    return {
      resumeLink: "https://google.com"
    };
  },
  mounted() {
    this.resumeLink = dataJson.resumeLink;
  },
  props: {
    solid: Boolean
  },
  methods: {
    goTop() {
      window.scroll({ left: 0, top: 0, behavior: "smooth" });
    }
  }
};
</script>

<style lang="scss">
nav {
  h3 {
    margin: 5px;
    cursor: pointer;
  }
  width: 100%;
  position: fixed;
  padding-right: 20px;
}
.nav-item {
  margin: 10px;
}
.solid {
  background-color: var(--q-bg);
  z-index: 10;
  transition: background-color 0.5s;
}

.fade-leave-active {
  animation: fade 1s;
}
.fade-enter-active {
  animation: fade 1s reverse;
}

@keyframes fade {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>
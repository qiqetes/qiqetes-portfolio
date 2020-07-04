<template>
  <div class="home">
    <Main />
    <About />
    <Work />
    <Skills />
  </div>
</template>

<script>
import About from "./About";
import Main from "./Main";
import Work from "./Work";
import Skills from "./Skills";

export default {
  components: {
    Main,
    Work,
    Skills,
    About
  }
};
</script>

<style lang="scss" scoped>
</style>

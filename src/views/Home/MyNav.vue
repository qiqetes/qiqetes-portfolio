<template>
  <nav :class="{solid: solid}">
    <ul class="nav justify-content-end">
      <li class="nav-item">Resume</li>
      <li class="nav-item">About me</li>
      <li class="nav-item">About me</li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    solid: Boolean
  }
};
</script>

<style lang="scss">
nav {
  width: 100%;
  position: fixed;
  padding-right: 20px;
}
.nav-item {
  margin: 10px;
}
.solid {
  background-color: white;
  z-index: 10;
  transition: background-color 0.5s;
}
</style>
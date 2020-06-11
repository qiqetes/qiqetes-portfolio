<template>
  <ul class="container">
    <div class="row justify-content-center">
      <li v-for="work in works" :key="work.name" class="col-5">
        <WorkCard :work="work" />
      </li>
    </div>
  </ul>
</template>

<script>
import workJson from "../../assets/work.json";
import WorkCard from "./WorkCard";

export default {
  data() {
    return {
      works: []
    };
  },
  mounted() {
    this.works = workJson.works;
  },
  components: {
    WorkCard
  }
};
</script>

<style>
</style>
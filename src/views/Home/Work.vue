<template>
  <div class="container">
    <h1 class="text-center">Some of my projects:</h1>
    <ul class="card-columns">
      <li v-for="work in works" :key="work.name" class="card">
        <WorkCard :work="work" />
      </li>
    </ul>
  </div>
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
    // TODO: add some kind of sort function to make the front-end projects appear first
    this.works = workJson.works;
  },
  components: {
    WorkCard
  }
};
</script>

<style lang="scss" scoped>
h1 {
  margin-top: 50px;
}
ul {
  margin-top: 40px;
}
.card-columns {
  column-count: 1;
}

.card {
  border: none;
}
@media (min-width: 768px) {
  .card-columns {
    column-count: 2;
  }
}
@media (min-width: 2400px) {
  .card-columns {
    column-count: 3;
  }
}
</style>
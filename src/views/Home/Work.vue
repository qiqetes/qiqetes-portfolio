<template>
  <div class="container" id="work" style="margin-top: 200px">
    <div class="row justify-content-start">
      <div class="col-lg-10 col-md-12">
        <h1>
          <span>02.</span> Some of my projects:
        </h1>
        <ul class="card-columns">
          <li v-for="work in works" :key="work.name" class="card">
            <WorkCard :work="work" :onClickTag="onClickChangeTag" :highlightedTag="highlightedTag" />
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import workJson from "../../assets/work.json";
import WorkCard from "./WorkCard";

export default {
  data() {
    return {
      works: [],
      highlightedTag: ""
    };
  },
  mounted() {
    // TODO: add some kind of sort function to make the front-end projects appear first
    this.works = workJson.works;
  },
  components: {
    WorkCard
  },
  methods: {
    onClickChangeTag(newTag) {
      if (newTag != this.highlightedTag) this.highlightedTag = newTag;
      else this.highlightedTag = "";
    }
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
</style>
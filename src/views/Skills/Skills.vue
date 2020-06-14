<template>
  <div class="container">
    <h1 class="text-center">Skills:</h1>

    <div class="row justify-content-center" style="margin-top: 40px">
      <div
        v-for="skill in skills"
        :key="skill.name"
        :class="'col-lg-' + 12/numRows + ' col-sm-' + 12/(numRows/2)"
      >
        <div class="row skill-card">
          <div class="col">
            <h3>{{skill.name}}</h3>
            <div class="break"></div>
            <ul>
              <li v-for="(subSkill,i) in skill.subskills" :key="subSkill">
                <span>{{i}}</span>
                {{subSkill}}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import workRaw from "../../assets/work.json";
export default {
  data() {
    return {
      skills: undefined,
      numRows: 0
    };
  },
  mounted() {
    this.skills = workRaw.skills;
    // FIX-ME will break if there are 5 groups :D
    this.numRows = this.skills.length;
  }
};
</script>

<style lang="scss" scoped>
@import "../../assets/scss/mixins.scss";
h1 {
  margin-top: 100px !important;
}
ul {
  padding-left: 10px;
  padding-top: 10px;
}
.break {
  height: 1px;
  background-color: var(--primary);
}
.skill-card {
  background-color: var(--q-sec);
  border-radius: 25px;
  margin: 12px;

  padding: 22px 18px 18px 15px;
  @include box-shadow(2);
  span {
    color: #a04f64;
  }
}
li:hover {
  background-color: rgba(0, 0, 0, 0.05);
  cursor: default;
}
</style>
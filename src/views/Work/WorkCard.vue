<template>
  <div class="work-card">
    <h4>{{work.name}}</h4>
    <p>{{work.description}}</p>
    <div class="row" style="margin: auto">
      <div class="col-sm-6 col-lg-8" style="padding: 0">
        <ul style="margin: 12px">
          <li v-for="tag in work.tags" :key="work.name+tag" class="tag">{{tag}}</li>
        </ul>
      </div>
      <div class="col-sm-6 col-lg-4 align-self-end" style="padding: 0">
        <div class="row justify-content-end">
          <Button style="padding: 4px 12px 4px 12px">
            source
            <i class="fas fa-code"></i>
          </Button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      work: undefined
    };
  },
  props: {
    work: Object
  },
  components: {}
};
</script>

<style lang="scss" scoped>
@import "../../assets/scss/mixins.scss";
.work-card {
  font-family: "Space Mono";
  li {
    display: inline-block;
    margin: 5px;
  }
  ul {
    padding-left: 0;
  }
  padding: 25px;
  border-radius: 30px;
  @include box-shadow(2);
}

.tag {
  font-size: 1em;
  padding: 2px;
  border-radius: 20px;
  padding: 2px 10px 2px 10px;
  color: white;
  background-color: rgb(53, 53, 53);
}
button {
  i {
    margin-left: 0;
  }
}
</style>

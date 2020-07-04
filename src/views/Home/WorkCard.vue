<template>
  <div class="work-card" :style="{opacity: transparency}">
    <h4>{{work.name}}</h4>
    <p>{{work.description}}</p>
    <div class="row" style="margin: auto">
      <div class="col-6 col-lg-7" style="padding: 0">
        <div class="row justify-content-start">
          <ul style="margin: 12px">
            <li v-for="tag in work.tags" :key="work.name+tag" class="tag">{{tag}}</li>
          </ul>
        </div>
      </div>
      <div class="col-6 col-lg-5 align-self-end" style="padding: 0">
        <!-- TODO: add a view live link -->
        <div class="row justify-content-end">
          <button v-if="work.link" v-on:click="goToLink(work.link)">
            source
            <i class="fas fa-code"></i>
          </button>
          <button v-if="!work.link" disabled>
            no source
            <i class="fas fa-code"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      transparency: 0,
      yIndex: 0,
      actual: 0,
      cT: this.changeTransparency
    };
  },
  created() {
    window.addEventListener("scroll", this.changeTransparency);
  },
  mounted() {
    this.yIndex = this.$el.getBoundingClientRect().top - window.innerHeight;
    this.changeTransparency;
  },
  props: {
    work: Object
  },
  methods: {
    goToLink(link) {
      window.open(link);
    },
    changeTransparency() {
      //  TODO: rename this method to eventHandler
      if (window.scrollY - 50 > this.yIndex && this.transparency != 1) {
        this.transparency = 1;
      } // FIXME: with enter it will behave better
    }
  }
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
  transition: opacity 1s;
  margin-bottom: 15px;
  background-color: var(--q-sec);
}

.tag {
  font-size: 1em;
  padding: 2px;
  border-radius: 20px;
  padding: 2px 10px 2px 10px;
  color: var(--q-sec);
  background-color: var(--q-tag);
  white-space: nowrap;
}
button {
  padding: 4px 12px 4px 12px;
  i {
    margin-left: 0;
  }
}
</style>

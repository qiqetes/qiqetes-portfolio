<template>
  <div class="work-card">
    <h5>{{work.name}}</h5>
    <p>{{work.description}}</p>
    <ul>
      <li v-for="tag in work.tags" :key="work.name+tag">{{tag}}</li>
    </ul>
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
  }
};
</script>

<style>
</style>
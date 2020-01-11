<template>
  <div class="RecommendationList">
    <ul>
      <li
        v-for="(recommendation, index) in recommendationResults"
        v-bind:key="index"
      >{{recommendation.name}} by {{recommendation.artists[0].name}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "RecommendationList",
  props: {
    recommendationResults: Array
  },
  created() {
    console.log("results:", this.recommendationResults);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>

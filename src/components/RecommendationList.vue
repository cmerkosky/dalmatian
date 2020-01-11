<template>
  <div class="RecommendationList">
    <ul>
      <li
        v-for="(recommendation, index) in recommendationResults"
        v-bind:key="index"
      ></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "RecommendationList",
  props: {
    recommendationResults: Array
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>

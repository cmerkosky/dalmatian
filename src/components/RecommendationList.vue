<template>
  <div class="RecommendationList">
    <ul>
      <li
        v-for="(recommendation, index) in recommendationResults"
        v-bind:key="index">
      <Song
        v-if="recommendation"
        :songInfo="recommendation">
      </Song>
      </li>
    </ul>
  </div>
</template>

<script>
import Song from "./Song.vue"
export default {
  name: "RecommendationList",
  components: {
    Song
  },
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

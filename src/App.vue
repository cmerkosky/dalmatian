<template>
  <div id="app">
    <RecommendationForm @formSubmit="handleFormSubmit"></RecommendationForm>
    <RecommendationList
      :recommendationResults="recommendationResults"
    ></RecommendationList>
  </div>
</template>

<script>
import RecommendationForm from "./components/RecommendationForm.vue";
import RecommendationList from "./components/RecommendationList.vue";

export default {
  name: "app",
  components: {
    RecommendationForm,
    RecommendationList
  },
  data() {
    return {
      recommendationResults: []
    };
  },
  created() {
    this.test();
  },
  methods: {
    handleFormSubmit() {
      window.location = "https://accounts.spotify.com/authorize?client_id=86a64fb12bc24841abd7312b1a462795&response_type=code&redirect_uri=http://localhost:8080";

    },
    test() {
      let params = new URLSearchParams(window.location.search.substring(1));
      console.log(params.get("code"));
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>

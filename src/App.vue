<template>
  <div id="app">
    <Splashscreen v-if="!authenticated"></Splashscreen>
    <RecommendationForm v-if="authenticated" @formSubmit="handleFormSubmit">
    </RecommendationForm>
    <RecommendationList
      v-if="authenticated"
      :recommendationResults="recommendationResults"
    ></RecommendationList>
  </div>
</template>

<script>
import RecommendationForm from "./components/RecommendationForm.vue";
import RecommendationList from "./components/RecommendationList.vue";
import Splashscreen from "./components/Splashscreen.vue";

export default {
  name: "app",
  components: {
    RecommendationForm,
    RecommendationList,
    Splashscreen
  },
  data() {
    return {
      recommendationResults: [],
      authenticated: false
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

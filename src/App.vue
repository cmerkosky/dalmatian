<template>
  <div id="app">
    <Splashscreen v-if="!authcode" @authenticate="authenticate"></Splashscreen>
    <RecommendationForm v-if="authcode" @formSubmit="handleFormSubmit">
    </RecommendationForm>
    <RecommendationList
      v-if="authcode"
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
      authcode: null
    };
  },
  created() {
    this.test();
    let params = new URLSearchParams(window.location.search.substring(1));
    this.authcode = params.get("code") 
    console.log(params.get("code"));
  },
  methods: {
    handleFormSubmit() {
      window.location = "https://accounts.spotify.com/authorize?client_id=86a64fb12bc24841abd7312b1a462795&response_type=code&redirect_uri=http://localhost:8080";
    },
    authenticate(){
      window.location = "https://accounts.spotify.com/authorize?client_id=86a64fb12bc24841abd7312b1a462795&response_type=code&redirect_uri=http://localhost:8080";
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

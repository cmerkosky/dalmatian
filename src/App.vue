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
    handleFormSubmit(data) {
      console.log(data);
    },
    test() {
      console.log("created!");
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

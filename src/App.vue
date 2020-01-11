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

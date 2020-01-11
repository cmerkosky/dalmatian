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
import axios from "axios";

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
      authcode: null,
      seed: ''
    };
  },
  created() {
    let params = new URLSearchParams(window.location.hash.substring(1));
    this.authcode = params.get("access_token");
    axios({
      method: "get",
      url: "https://api.spotify.com/v1/me/top/tracks?limit=5",
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
        Authorization: "Bearer "+ this.authcode
      }
    })
    .then(response=>{
      response.data.items.forEach(element => {
        this.seed = this.seed + element.id + ','
      });
      this.seed = this.seed.substring(0,this.seed.length-1);
    })
  },
  methods: {
    handleFormSubmit(data) {
      console.log(data);
      axios({
        method: "get",
        url: "https://api.spotify.com/v1/recommendations",
        params: {
          market: "US",
          seed_tracks: this.seed,
          ...data
        },
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
          Authorization: "Bearer " + this.authcode
        }
      })
      .then(response => {
        console.log(response.data)
        this.recommendationResults = response.data.tracks;
      })
      .catch(e => {
        console.log(e)
      })
    },
    authenticate(){
      window.location = "https://accounts.spotify.com/authorize?client_id=86a64fb12bc24841abd7312b1a462795&response_type=token&redirect_uri=http://localhost:8080";
    }
  }
};
</script>

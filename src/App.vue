<template>
  <div id="app" class="main-content">
    <Splashscreen v-if="!authcode" @authenticate="authenticate"></Splashscreen>
    <div v-else class="app-area">
      <div v-if="authcode" class="header-bar">
        <header>
          <h1>Dalmation</h1>
        </header>
      </div>
      <div class="body-area">
        <div class="row">
          <div class="column left">
            <RecommendationForm @formSubmit="handleFormSubmit">
            </RecommendationForm>
          </div>
          <div class="column right">
            <RecommendationList
              :recommendationResults="recommendationResults"
            ></RecommendationList>
          </div>
        </div>
      </div>
    </div>
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
      authcode: null
    };
  },
  created() {
    let params = new URLSearchParams(window.location.hash.substring(1));
    this.authcode = params.get("access_token");
    console.log(params.get("access_token"));
    axios({
      method: "get",
      url: "https://api.spotify.com/v1/recommendations?market=US&seed_artists=4NHQUGzhtTLFvgF5SZesLK",
      data: {
        seed_artists: "4NHQUGzhtTLFvgF5SZesLK"
      },
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
        Authorization: "Bearer " + this.authcode
      }
    })
    .then(response => {
      console.log(response.data)
    })
    .catch(e => {
      console.log(e)
    })
  },
  methods: {
    handleFormSubmit() {
      
    },
    authenticate(){
      window.location = "https://accounts.spotify.com/authorize?client_id=86a64fb12bc24841abd7312b1a462795&response_type=token&redirect_uri=http://localhost:8080";
    }
  }
};
</script>

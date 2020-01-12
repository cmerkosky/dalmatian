<template>
  <div id="app" class="main-content">
    <Splashscreen v-if="!authcode" @authenticate="authenticate"></Splashscreen>
    <div v-else class="app-area">
      <div v-if="authcode" class="header-bar">
        <header @click="logout">
          <h1><span class="header-text">Dalmation</span></h1>
        </header>
      </div>
      <div class="body-area">
        <div class="column-row">
          <div class="column column-left ui-section">
            <RecommendationForm @formSubmit="handleFormSubmit">
            </RecommendationForm>
          </div>
          <div v-if="recommendationResults.length > 0" class="column column-right ui-section">
            <RecommendationList
              :recommendationResults="recommendationResults"
              @createPlaylist="createPlaylist"
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
      authcode: null,
      seed: [],
      user: null
    };
  },
  created() {
    let params = new URLSearchParams(window.location.hash.substring(1));
    this.authcode = params.get("access_token");
    axios({
      method: "get",
      url: "https://api.spotify.com/v1/me",
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
        Authorization: "Bearer " + this.authcode
      }
    })
    .then(response=>{
      this.user = response.data
      console.log(this.user)
    })
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
      this.seed = response.data.items
    })
  },
  methods: {
    logout() {
      this.authcode = null
      this.recommendationResults = []
      this.seed = []
      this.user = null
      window.location = window.location.origin
    },
    handleFormSubmit(formData) {
      console.log(formData);
      console.log(this.seed);
      axios({
        method: "get",
        url: "https://api.spotify.com/v1/recommendations",
        params: {
          market: "US",
          seed_tracks: this.seed.reduce(function(tracks, element) {
            return tracks + element.id + ','
          }, ''),
          ...formData,
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
    createPlaylist() {
      axios({
        method: "post",
        url: "https://api.spotify.com/v1/users/" + this.user.id + "/playlists",
        headers: {
          Authorization: "Bearer " + this.authcode,
          "Content-Type": "application/json",
          Accept: "application/json"
        },
        data: {
          name: "Dalmation playlist"
        }
      })
      .then(response=>{
        axios({
          method: "post",
          url: "https://api.spotify.com/v1/playlists/" + response.data.id +"/tracks",
          headers: {
            Authorization: "Bearer " + this.authcode,
            "Content-Type": "application/json",
            Accept: "application/json"
          },
          data: {
            "uris": this.recommendationResults.map(result => "spotify:track:"+result.id)
          }
        })
        .then(()=>{
          console.log(response)
          window.open(response.data.external_urls.spotify, "_blank")
        })
      })
    },
    authenticate(){
      let redirectUri = window.location.href.includes("localhost") ? "http://localhost:8080" : "https://dalmation.netlify.com"
      window.location = `https://accounts.spotify.com/authorize?client_id=86a64fb12bc24841abd7312b1a462795&response_type=token&redirect_uri=${redirectUri}&scope=user-top-read%20playlist-modify-public`;
    }
  }
};
</script>

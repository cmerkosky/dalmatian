<template>
  <div class="RecommendationList">
    <ul class="song-list">
      <li
        v-for="(recommendation, index) in recommendationResults"
        v-bind:key="index">
        <div class="song-item">
          <div class="song-artwork">
              <img :src="recommendation.album.images[2].url" class="image"/>
              <div class="play-button">
                <i class="fa fa-play-circle"></i>
              </div>
          </div>
          <div class="song-details">
              <h3>{{recommendation.name}}</h3>
              <p>{{recommendation.artists[0].name}}</p>
          </div>
          <a :href="'http://open.spotify.com/track/' + recommendation.id" target="_blank" rel="noopener noreferrer" class="hidden-link"/>
        </div>
      </li>
    </ul>
    <button @click="createPlaylist" class="action-button">Create Playlist</button>
  </div>
</template>

<script>
export default {
  name: "RecommendationList",
  props: {
    recommendationResults: Array
  },
  created() {
    console.log("results:", this.recommendationResults);
  },
  methods: {
    createPlaylist() {
      this.$emit("createPlaylist")
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>

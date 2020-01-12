<template>
  <div class="RecommendationForm">
    <form @submit="handleSubmit" id="recommendation-form">
      <ul class=control-list>
        <li>
          <div class="input-block">
            <label for="danceability" class="controller-label">Danceability</label>
            <div class="slider-box">
              <label for="danceability" class="end-label">Min</label>
              <input id="danceability" class="input-slider" v-model="danceability" type="range" min="0" max="1" step="0.01" />
              <label for="danceability" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <label for="energy" class="controller-label">energy</label>
            <div class="slider-box">
              <label for="energy" class="end-label">Min</label>
              <input id="energy" class="input-slider" v-model="energy" type="range" min="0" max="1" step="0.01" />
              <label for="energy" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <label for="instrumentalness" class="controller-label">instrumentalness</label>
            <div class="slider-box">
              <label for="instrumentalness" class="end-label">Min</label>
              <input id="instrumentalness" class="input-slider" v-model="instrumentalness" type="range" min="0" max="1" step="0.01" />
              <label for="instrumentalness" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <label for="popularity" class="controller-label">popularity</label>
            <div class="slider-box">
              <label for="popularity" class="end-label">Min</label>
              <input id="popularity" class="input-slider" v-model="popularity" type="range" min="0" max="100" step="1" />
              <label for="popularity" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <label for="valence" class="controller-label">happiness</label>
            <div class="slider-box">
              <label for="valence" class="end-label">Min</label>
              <input id="valence" class="input-slider" v-model="valence" type="range" min="0" max="1" step="0.01" />
              <label for="valence" class="end-label">Max</label>
            </div>
          </div>
        </li>
      </ul>
    </form>
    <button action="submit" form="recommendation-form" class="action-button" style="margin-right: 10px">Hit it</button>
    <button @click='resetForm' class="action-button">Reset</button>
  </div>
</template>

<script>
export default {
  name: "RecommendationForm",
  data() {
    return {
      danceability: 0.5,
      energy: 0.5,
      instrumentalness: 0.5,
      popularity: 50,
      valence: 0.5,
    };
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault();
      this.$emit("formSubmit", { 
        target_danceability: this.danceability,
        target_energy: this.energy,
        target_instrumentalness: this.instrumentalness,
        target_popularity: this.popularity,
        target_valence: this.valence, 
      });
    },
    resetForm() {
      this.danceability = 0.5;
      this.energy = 0.5;
      this.instrumentalness = 0.5;
      this.popularity = 50;
      this.valence = 0.5;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  form {
    color: white;
  }
  label {
    font-weight: bold;
  }
  ul {
    list-style: none;
  }
  li {
    margin: 1rem 0;
  }
</style>

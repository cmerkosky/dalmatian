<template>
  <div class="RecommendationForm">
    <form @submit="handleSubmit" id="recommendation-form">
      <ul class=control-list>
        <li>
          <div class="input-block">
            <input type="checkbox" id="danceability-checkbox" v-model="danceabilityChecked" class="checkbox"/>
            <label for="danceability-checkbox" class="controller-label">Danceability</label>
            <div class="slider-box">
              <label for="danceability" class="end-label">Min</label>
              <input id="danceability" class="input-slider" v-model="danceability" type="range" min="0" max="1" step="0.01" />
              <label for="danceability" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <input type="checkbox" id="energy-checkbox" v-model="energyChecked" class="checkbox"/>
            <label for="energy-checkbox" class="controller-label">energy</label>
            <div class="slider-box">
              <label for="energy" class="end-label">Min</label>
              <input id="energy" class="input-slider" v-model="energy" type="range" min="0" max="1" step="0.01" />
              <label for="energy" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <input type="checkbox" id="instrumentalness-checkbox" v-model="instrumentalnessChecked" class="checkbox"/>
            <label for="instrumentalness-checkbox" class="controller-label">instrumentalness</label>
            <div class="slider-box">
              <label for="instrumentalness" class="end-label">Min</label>
              <input id="instrumentalness" class="input-slider" v-model="instrumentalness" type="range" min="0" max="1" step="0.01" />
              <label for="instrumentalness" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <input type="checkbox" id="popularity-checkbox" v-model="popularityChecked" class="checkbox"/>
            <label for="popularity-checkbox" class="controller-label">popularity</label>
            <div class="slider-box">
              <label for="popularity" class="end-label">Min</label>
              <input id="popularity" class="input-slider" v-model="popularity" type="range" min="0" max="100" step="1" />
              <label for="popularity" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <input type="checkbox" id="valence-checkbox" v-model="valenceChecked" class="checkbox"/>
            <label for="valence-checkbox" class="controller-label">happiness</label>
            <div class="slider-box">
              <label for="valence" class="end-label">Min</label>
              <input id="valence" class="input-slider" v-model="valence" type="range" min="0" max="1" step="0.01" />
              <label for="valence" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <input type="checkbox" id="acousticness-checkbox" v-model="acousticnessChecked" class="checkbox"/>
            <label for="acousticness-checkbox" class="controller-label">acousticness</label>
            <div class="slider-box">
              <label for="acousticness" class="end-label">Min</label>
              <input id="acousticness" class="input-slider" v-model="acousticness" type="range" min="0" max="1" step="0.01" />
              <label for="acousticness" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <input type="checkbox" id="liveness-checkbox" v-model="livenessChecked" class="checkbox"/>
            <label for="liveness-checkbox" class="controller-label">liveness</label>
            <div class="slider-box">
              <label for="liveness" class="end-label">Min</label>
              <input id="liveness" class="input-slider" v-model="liveness" type="range" min="0" max="1" step="0.01" />
              <label for="liveness" class="end-label">Max</label>
            </div>
          </div>
        </li>

        <li>
          <div class="input-block">
            <input type="checkbox" id="loudness-checkbox" v-model="loudnessChecked" class="checkbox"/>
            <label for="loudness-checkbox" class="controller-label">loudness</label>
            <div class="slider-box">
              <label for="loudness" class="end-label">Min</label>
              <input id="loudness" class="input-slider" v-model="loudness" type="range" min="-60" max="0" step="0.1" />
              <label for="loudness" class="end-label">Max</label>
            </div>
          </div>
        </li>
      </ul>
    </form>
    <button action="submit" form="recommendation-form" class="action-button">Hit it</button>
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
      acousticness: 0.5,
      liveness: 0.5,
      loudness: -30,
      danceabilityChecked: true,
      energyChecked: true,
      instrumentalnessChecked: true,
      popularityChecked: true,
      valenceChecked: true,
      acousticnessChecked: true,
      livenessChecked: true,
      loudnessChecked: true,
    };
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault();
      this.$emit("formSubmit", this.buildFormData());
      window.scrollTo(0,document.body.scrollHeight);
    },
    resetForm() {
      this.danceability = 0.5;
      this.energy = 0.5;
      this.instrumentalness = 0.5;
      this.popularity = 50;
      this.valence = 0.5;
      this.acousticness = 0.5;
      this.loudness = -30;
      this.liveness = 0.5;
      this.danceabilityChecked = true;
      this.energyChecked = true;
      this.instrumentalnessChecked = true;
      this.popularityChecked = true;
      this.valenceChecked = true;
      this.acousticnessChecked = true;
      this.livenessChecked = true;
      this.loudnessChecked = true;
    },
    buildFormData(){
      let data = {}
      if(this.danceabilityChecked){
        data.target_danceability = this.danceability
      }
      if(this.energyChecked){
        data.target_energy = this.energy
      }
      if(this.instrumentalnessChecked){
        data.target_instrumentalness = this.instrumentalness
      }
      if(this.popularityChecked){
        data.target_popularity = this.popularity
      }
      if(this.valenceChecked){
        data.target_valence = this.valence
      }
      if(this.acousticnessChecked){
        data.target_acousticness = this.acousticness
      }
      if(this.livenessChecked){
        data.target_liveness = this.liveness
      }
      if(this.loudnessChecked){
        data.target_loudness = this.loudness
      }
      return data
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

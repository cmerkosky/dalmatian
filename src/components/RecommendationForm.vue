<template>
  <div class="RecommendationForm">
    <form @submit="handleSubmit">
      <ul>
        <li>
          <label for="danceability" class="controller-label">Danceability</label><br>
          min <input id="danceability" class="input-slider" v-model="danceability" type="range" min="0" max="1" step="0.01" /> max
        </li>
        <li>
          <label for="Energy" class="controller-label">Energy</label><br>
          min <input id="energy" class="input-slider" v-model="energy" type="range" min="0" max="1" step="0.01" /> max
        </li>
        <li>
          <label for="instrumentalness" class="controller-label">Instrumentalness</label><br>
          min <input id="instrumentalness" class="input-slider" v-model="instrumentalness" type="range" min="0" max="1" step="0.01" /> max
        </li>
        <li>
          <label for="popularity" class="controller-label">Popularity</label><br>
          min <input id="popularity" class="input-slider" v-model="popularity" type="range" min="0" max="100" step="1" /> max
        </li>
        <li>
          <label for="valence" class="controller-label">Positivity</label><br>
          min <input id="valence" class="input-slider" v-model="valence" type="range" min="0" max="1" step="0.01" /> max
        </li>
      </ul>
    </form>
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
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  form {
    color: white;
  }
  ul {
    list-style: none;
  }
  li {
    margin: 1rem 0;
  }
</style>

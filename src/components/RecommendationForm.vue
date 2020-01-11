<template>
  <div class="RecommendationForm">
    <form @submit="handleSubmit">
      <label class="controller-label">
        Danceability
        <input v-model="danceability" type="range" min="0" max="1" step="0.01" class="input-slider" />
      </label>
    </form>
  </div>
</template>

<script>
export default {
  name: "RecommendationForm",
  data() {
    return {
      danceability: 0.5
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
<style scoped></style>

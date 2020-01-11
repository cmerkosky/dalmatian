<template>
  <div class="RecommendationForm">
    <form @submit="handleSubmit">
      <label>
        Danceability: {{danceability}}
        <input v-model="danceability" type="range" min="0" max="1" step="0.1" />
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

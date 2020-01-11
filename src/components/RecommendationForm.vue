<template>
  <div class="RecommendationForm">
    <form @submit="handleSubmit">
      <label>
        Title:
        <input v-model="title" />
      </label>
    </form>
  </div>
</template>

<script>
export default {
  name: "RecommendationForm",
  data() {
    return {
      title: ""
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

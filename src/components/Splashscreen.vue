<template>
  <div class="Splashscreen">
    <div class="content">
        <div class="splashscreen-text-container">
            <h1 class="site-title">Dalmation</h1>
            <h3 class="site-subtitle">Your music's best friend</h3>
            <button @click="handleButtonClick" class="action-button">Enter</button>
        </div>
      </div>
  </div>
</template>

<script>
export default {
    methods:{
        handleButtonClick(){
            this.$emit("authenticate")
        }
    }
}
</script>
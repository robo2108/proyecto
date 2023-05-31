<script setup>
import { ref } from "vue";
const sliderValue = ref(50);
</script>

<template>
  <header class="header">
    Control
  </header>
  <div class="custom-slider">
    <input v-model="sliderValue" type="number" class="input" />
    <br>
    <input
      v-model="sliderValue"
      type="range"
      min="0"
      max="100"
      class="slider"
    />
   
  </div>

</template>
<style scoped>


</style>

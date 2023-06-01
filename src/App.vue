<script setup>
import { ref } from "vue";
const sliderValue = ref(50);
const direccion = ref(0);


</script>



<template>
  <header class="header">Control</header> 
  <button v-on:click="direccion= 0">Stop</button>
  <button v-on:click="direccion= 1">Forward</button>
  <button v-on:click="direccion= -1">Reverse</button>

  <p>Direccion {{ direccion }}</p>
  <div class="custom-slider">
  <input v-model="sliderValue" type="number" />
  <br />
  <input v-model="sliderValue" type="range" min="0" max="100" class="slider" />


</div>
</template>


<script setup>
import { ref } from "vue";
const sliderValue = ref(50);
const direccion = ref(0);


</script>



<template>
  <header class="titulomain">DESARROLLO DE TELECOMUNICACIONES Y SISTEMAS ENERGÉTICOS</header>
  <h1 class="titulosubmain">APLICACIÓN DE IOE A UNA CIUDAD INTELIGENTE</h1>

  <header class="header">Control</header> 
  <button v-on:click="direccion= 0">Stop</button>
  <button v-on:click="direccion= 1">Forward</button>
  <button v-on:click="direccion= -1">Reverse</button>

  <p class="titulo">Direccion {{ direccion }}</p>
  <div class="custom-slider">
  <input v-model="sliderValue" type="number" />
  <br />
  <input v-model="sliderValue" type="range" min="0" max="100" class="slider" />

  


</div>
</template>




<script setup>
import { ref } from "vue";
import { initializeApp } from 'firebase/app';
import { getDatabase, ref, set } from "firebase/database";
const firebaseConfig = {
  apiKey: "AIzaSyB3JFucQNPGMnScIQNBcrTgb5fskIss5Jc",
  authDomain: "esp32motorcontrol-95da1.firebaseapp.com",
  databaseURL: "https://esp32motorcontrol-95da1-default-rtdb.firebaseio.com",
  projectId: "esp32motorcontrol-95da1",
  storageBucket: "esp32motorcontrol-95da1.appspot.com",
  messagingSenderId: "1096988131286",
  appId: "1:1096988131286:web:7bbd472cc6fbb04c4f6e77",
  measurementId: "G-JT0QTTRR7X"
};

const sliderValue = ref(50);
const direccion = ref(0);
const velocidad = ref(0);
const app= initializeApp(firebaseConfig)
const db = getDatabase(app);
set(ref(db, 'Comandos/'), {
    Direccion:direccion
  });


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
  <p>Velocidad {{ velocidad }}</p>
  


</div>
</template>


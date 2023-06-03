<script setup>
import { ref as vueref} from "vue";
import { initializeApp } from 'firebase/app';
import { getDatabase, set, ref } from "firebase/database";
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

const sliderValue = vueref(50);


const direccion = vueref(0);
const app = initializeApp(firebaseConfig);
const db = getDatabase(app);

const updateDireccion = (value) => {
  direccion.value = value;
  set(ref(db, '/Comandos/Direccion'), direccion.value)
    .then(() => {
      console.log('Value set in Firebase');
    })
    .catch((error) => {
      console.error('Error setting value in Firebase:', error);
    });
};


</script>



<template>
  <header class="titulomain">DESARROLLO DE TELECOMUNICACIONES Y SISTEMAS ENERGÉTICOS</header>
  <h1 class="titulosubmain">APLICACIÓN DE IOE A UNA CIUDAD INTELIGENTE</h1>

  <header class="header">Control</header> 
  <button v-on:click="updateDireccion(0)">Stop</button>
  <button v-on:click="updateDireccion(1)">Forward</button>
  <button v-on:click="updateDireccion(-1)">Reverse</button>

  <p class="titulo">Direccion {{ direccion }}</p>
  <div class="custom-slider">
  <input v-model="sliderValue" type="number" />
  <br />
  <input v-model="sliderValue" type="range" min="0" max="100" class="slider" />

  <p>{{ velocidad }}</p>
  <p>Velocidad </p>
  <p>0</p>
  <p>Voltaje </p>
  <p>0</p>
  <p>Corriente</p>
  
  

  


</div>
</template>




<script setup>
import { ref as vueref, watchEffect } from "vue";
import { initializeApp } from "firebase/app";
import { getDatabase, ref, set, get } from "firebase/database";
import Chart from 'chart.js/auto';
const firebaseConfig = {
  apiKey: "AIzaSyB3JFucQNPGMnScIQNBcrTgb5fskIss5Jc",
  authDomain: "esp32motorcontrol-95da1.firebaseapp.com",
  databaseURL: "https://esp32motorcontrol-95da1-default-rtdb.firebaseio.com",
  projectId: "esp32motorcontrol-95da1",
  storageBucket: "esp32motorcontrol-95da1.appspot.com",
  messagingSenderId: "1096988131286",
  appId: "1:1096988131286:web:7bbd472cc6fbb04c4f6e77",
  measurementId: "G-JT0QTTRR7X",
};

const sliderValue = vueref(0);

const direccion = vueref(0);
const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
const chartCanvas = vueref(null);

const updateDireccion = (value) => {
  direccion.value = value;
  set(ref(db, "/Comandos/Direccion"), direccion.value)
    .then(() => {
      console.log("Value set in Firebase");
    })
    .catch((error) => {
      console.error("Error setting value in Firebase:", error);
    });
};


const updateVelocidad = (newValue) => {
  if (sliderValue== undefined){
    var newValue=50
  }
  else{
  newValue=parseInt(sliderValue.value);
  }
  set(ref(db, '/Comandos/Velocidad'), newValue)
  .then(() => {
      console.log("Value set in Firebase");
    })
    .catch((error) => {
      console.error("Error setting value in Firebase:", error);
    });
};

const firebaseRef = ref(db, '/Mediciones/Velocidad');
get(firebaseRef).then((snapshot) => {
     const data = snapshot.val();
      createBarChart(data);
    }).catch((error) => {
      console.error(error);
    });

    const createBarChart = (data) => {
      const labels = Object.keys(data);
      const values = Object.values(data);

      new Chart(chartCanvas.value, {
        type: 'bar',
        data: {
          labels: labels,
          datasets: [
            {
              label: 'Values',
              data: values,
              backgroundColor: 'rgba(75, 192, 192, 0.2)',
              borderColor: 'rgba(75, 192, 192, 1)',
              borderWidth: 1
            }
          ]
        },
        options: {
          responsive: true,
          scales: {
            x: {
              type: 'category',
              labels: labels
            },
            y: {
              beginAtZero: true
            }
          }
        }
      });
    };

</script>

<template>
   <div class="line-1"></div>
  <div class="linea-vertical"></div>
  <div class="line-2"></div>
  <header class="titulomain">
    DESARROLLO DE TELECOMUNICACIONES Y SISTEMAS ENERGÉTICOS
  </header>
  <h1 class="titulosubmain">APLICACIÓN DE IOE A UNA CIUDAD INTELIGENTE</h1>
  <header class="headerp">Control</header>
  <header class="headerp2">Sensado</header>
  <header class="headerp3">Visualización</header>
 
  <button class="redondo1" v-on:click="updateDireccion(0)">Stop</button>
  <button class="redondo2" v-on:click="updateDireccion(1)">Forward</button>
  <button class="redondo3" v-on:click="updateDireccion(2)">Reverse</button>

  
  <p class="direc">Direccion {{ direccion }}</p>
  <div class="custom-slider">
    <input  class="velo"  v-on:change="updateVelocidad" v-model="sliderValue" type="number" />
    <br />
    <input
    v-on:change="updateVelocidad"
      v-model="sliderValue"
      type="range"
      min="0"
      max="100"
      class="slider"
    />

    <p>{{ velocidad }}</p>
    <p class="velopo">Velocidad</p>
    <p class="veloponum">0</p>
    <p class="volpo">Voltaje</p>
    <p class="volponum">0</p>
    <p class="corrpo">Corriente</p>
    <p class="corrponum">0</p>
  </div>

  <div class="radio-container" style="top: 15px; left: 680px;">
  <input type="radio" id="radio1" name="radio-group">
  <label for="radio1" class="radio-label">Velocidad</label>
  </div>

  <div class="radio-container" style="top: 15px; left: 680px;">
  <input type="radio" id="radio2" name="radio-group">
  <label for="radio2" class="radio-label">Voltaje</label>
  </div>

  <div class="radio-container" style="top: 15px; left: 680px;">
  <input type="radio" id="radio3" name="radio-group">
  <label for="radio3" class="radio-label">Corriente</label>
  </div>
  <canvas ref="chartCanvas"></canvas>

</template>

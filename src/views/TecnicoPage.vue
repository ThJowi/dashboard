<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>📈 Técnico</ion-title>
      </ion-toolbar>
    </ion-header>


    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">📈 Técnico</ion-title>
        </ion-toolbar>
      </ion-header>

 <!-- Grid principal del Dashboard -->
      <ion-grid class="dashboard-grid">
        <!-- 🟢 Fila 1: 4 Columnas -->
        <ion-row class="ion-row-1">
          <ion-col size="12" size-lg="4">
            <div class="box">
              <spark-line v-bind="sparkData1"/>
            </div>
          </ion-col>
          <ion-col size="6" size-lg="4">
            <div class="box">
              <spark-line v-bind="sparkData2"/>
            </div>
          </ion-col>
          <ion-col size="6" size-lg="4">
            <div class="box">
              <spark-line v-bind="sparkData3"/>
            </div>
          </ion-col>
        </ion-row>


        <!-- 🔵 Fila 2: 2 Columnas -->
        <ion-row class="ion-row-2">
          <ion-col size="12" size-md="3" push-md="9">
            <div class="box">
              CPU
              <RTSpeedGauge :interval = "500"/>
            </div>
          </ion-col>
            <ion-col size="12" size-md="9" pull-md="3">
              <div class="box">
                <RTLineChart :interval = "1000"/>
              </div>
            </ion-col>
        </ion-row>


        <!-- 🟠 Fila 3: 2 Columnas -->
        <ion-row class="ion-row-3">
          <ion-col size="12" size-lg="4">
            <div class="box">
              Uso de RAM (%)
              <LineChart
                :labels="lineLabels1"
                :values="lineValues1"
              />
              
            </div>
          </ion-col>
          <ion-col size="12" size-lg="4">
            <div class="box">
              <BarChart
                :chart-data="barChartData"
                :options="barChartOptions"
                />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="4">
            <div class="box">
              Tasa de disponibilidad
              <LineChart
                :labels="lineLabels2"
                :values="lineValues2"
              />
            </div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { ref } from 'vue';
import SparkLine from '@/components/SparkLine.vue';
import RTSpeedGauge from '@/components/RTSpeedGauge.vue';
import RTLineChart from '@/components/RTLineChart.vue';
import BarChart from '@/components/BarChart.vue';
import LineChart from '@/components/LineChart.vue';

const sparkData1 = ref({
  /* Propiedades del componente */
  title: "Errores (por cada 1000 peticiones)",
  value: "8.2",
  bgColor: "gradient-pink",
  textColor: "white",
  iconName: "bug",
  /* Propiedades del componentes interno de ApexChart */
  chartOptions: {
    chart: {
      id: 'errores',
      type: '',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'straight', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [50, 20, 15, 12, 11, 8] }],
});

const sparkData2 = ref({
  /* Propiedades del componente */
  title: "Pico de usuarios",
  value: "4529",
  bgColor: "gradient-orange",
  textColor: "white",
  iconName: "people-outline",
  /* Propiedades del componentes interno de ApexChart */
  chartOptions: {
    chart: {
      id: 'picoUsuarios',
      type: '',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [3295, 1039, 1294, 1132, 2809, 4529] }],
});

const sparkData3 = ref({
  /* Propiedades del componente */
  title: "Pico de peticiones (por minuto)",
  value: "673",
  bgColor: "gradient-blue",
  textColor: "white",
  iconName: "bag",
  /* Propiedades del componentes interno de ApexChart */
  chartOptions: {
    chart: {
      id: 'picoPeticiones',
      type: 'bar',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [538, 203, 195, 234, 289, 673] }],
});

const barChartData = {
  labels: ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio'],
  datasets: [
    {
      label: 'Errores',
      data: [753, 318, 89, 63, 53, 38],
      backgroundColor: 'rgba(75, 192, 192, 0.6)',
      borderColor: 'rgba(75, 192, 192, 1)',
      borderWidth: 1
    }
  ]
};
const barChartOptions = {
  scales: {
    y: {
      beginAtZero: true
    }
  }
};

const lineLabels1 = ['Ene','Feb','Mar','Abr','May','Jun'];
const lineValues1 = [86, 43, 52, 67, 75 , 64];

const lineLabels2 = ['Ene','Feb','Mar','Abr','May','Jun'];
const lineValues2 = [63, 95, 97, 89, 84 , 99];
</script>

<style scoped>


ion-row{
  overflow: hidden;
}


ion-col {
  max-height: 100%;
  --ion-grid-column-padding:10px;
}


/* El contenido real de cada columna */
.box {
  background: #1E1E1E;
  height: 100%;
  max-height: 100%;
  overflow: hidden;
  border-radius:5px;
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
}


/* Aplicar altura total y por filas, solo en pantallas ≥ md */
@media (min-width: 992px) {  
  ion-grid{height: 100%;}
  .ion-row-1{height: 20%; max-height: 20%;}
  .ion-row-2{height: 40%; max-height: 40%;}
  .ion-row-3{height: 40%; max-height: 40%;}
}


</style>

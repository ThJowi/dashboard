<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>🚀 Negocio</ion-title>
      </ion-toolbar>
    </ion-header>


    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">🚀 Negocio</ion-title>
        </ion-toolbar>
      </ion-header>

       <!-- Grid principal del Dashboard -->
      <ion-grid class="dashboard-grid">
        <!-- 🟢 Fila 1: 4 Columnas -->
        <ion-row class="ion-row-1">
          <ion-col size="6" size-lg="3">
           <div class="box">
              <spark-line v-bind="sparkData1"/>
            </div>
          </ion-col>
          <ion-col size="6" size-lg="3">
            <div class="box">
               <spark-line v-bind="sparkData2"/>
            </div>
          </ion-col>
          <ion-col size="6" size-lg="3">
            <div class="box">
               <spark-line v-bind="sparkData3"/>
            </div>
          </ion-col>
          <ion-col size="6" size-lg="3">
            <div class="box">
               <spark-line v-bind="sparkData4"/>
            </div>
          </ion-col>
        </ion-row>


        <!-- 🔵 Fila 2: 2 Columnas -->
        <ion-row class="ion-row-2">
          <ion-col size="12" size-lg="9">
            <div class="box">
              Pedidos en tiempo real
              <RTLineChart
                :interval = "5000"
                :offset = "10"
              />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="3">
            <div class="box">
              <PieChart 
                :series="pieSeries" 
                :labels="pieLabels" 
              />
            </div>
          </ion-col>
        </ion-row>


        <!-- 🟠 Fila 3: 2 Columnas -->
        <ion-row class="ion-row-3">
          <ion-col size="12" size-lg="6">
            <div class="box">
              <BarChart
                :chart-data="barChartData"
                :options="barChartOptions"
              />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="6">
            <div class="box">
              <MixedChart
                :labels="mixedLabels"
                :orders="mixedBarValues"
                :repeatRate="mixedLineValues"
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
import SparkLine from '@/components/SparkLine.vue';
import { ref } from 'vue';
import BarChart from '@/components/BarChart.vue'
import PieChart from '@/components/PieChart.vue';
import RTLineChart from '@/components/RTLineChart.vue';
import MixedChart from '@/components/MixedChart.vue';

const sparkData1 = ref({
  /* Propiedades del componente */
  title: "Pedidos",
  value: "15480",
  bgColor: "gradient-orange",
  textColor: "white",
  iconName: "bag",
  /* Propiedades del componentes interno de ApexChart */
  chartOptions: {
    chart: {
      id: 'pedidos',
      type: 'area',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [2300, 1800, 2740, 2360, 2780, 3500] }],
});

const sparkData2 = ref({
  /* Propiedades del componente */
  title: "Ingresos",
  value: "190k",
  bgColor: "gradient-green",
  textColor: "white",
  iconName: "cash-outline",
  /* Propiedades del componentes interno de ApexChart */
  chartOptions: {
    chart: {
      id: 'ingresos',
      type: '',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [24000, 43000, 81000, 112000, 148000, 190000] }],
});

const sparkData3 = ref({
  /* Propiedades del componente */
  title: "Usuarios",
  value: "14107",
  bgColor: "gradient-pink",
  textColor: "white",
  iconName: "people-outline",
  /* Propiedades del componentes interno de ApexChart */
  chartOptions: {
    chart: {
      id: 'Usuarios',
      type: 'bar',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [4114, 2367, 1832, 1371, 1619, 2804] }],
});

const sparkData4 = ref({
  /* Propiedades del componente */
  title: "Restaurantes",
  value: "87",
  bgColor: "gradient-blue",
  textColor: "white",
  iconName: "restaurant",
  /* Propiedades del componentes interno de ApexChart */
  chartOptions: {
    chart: {
      id: 'Restaurantes',
      type: '',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'straight', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [20, 5, 16, 9, 10, 27] }],
});

const barChartData = {
  labels: ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio'],
  datasets: [
    {
      label: 'Ventas (€)',
      data: [30000, 24000, 48000, 38000, 46000, 52000],
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

const pieSeries = [27.7, 35.5, 8.4, 28.4];
const pieLabels = ['Pizza','Hamburguesas','Ensaladas','Sushi'];



const mixedLabels = ['Ene','Feb','Mar','Abr','May','Jun'];
const mixedBarValues = [2300, 1800, 2740, 2360, 2780, 3500]
const mixedLineValues = [12, 18, 24, 29, 31, 33, 100];

</script>



<style scoped>


ion-row{
  overflow: hidden;
  /*border: 1px solid red;*/
}


ion-col {
  max-height: 100%;
  --ion-grid-column-padding:10px;
  /*background-color: blue;*/
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
  justify-content: center;
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


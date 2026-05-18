<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>🎯 KPIs</ion-title>
      </ion-toolbar>
    </ion-header>


    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">🎯 KPIs</ion-title>
        </ion-toolbar>
      </ion-header>


      <h1 class="ion-padding">🚀 KPIs de Negocio</h1>
      <ion-accordion-group expand="inset" :multiple="true">
        <ion-accordion v-for="item in smartGoalsBusiness" :key="item.id" :value="item.id.toString()">
          <ion-item slot="header">
            <ion-label>{{ item.id }}. {{ item.title }}</ion-label>
          </ion-item>
          <div class="ion-padding" slot="content">
            <p>{{ item.description }}</p>
            <ion-list :inset="true">
              <ion-item v-for="(element, index) in item.smart" :key="index">
                <ion-label><b>{{ element.letter }}</b> → {{ element.content }}</ion-label>
              </ion-item>
            </ion-list>
          </div>
        </ion-accordion>
      </ion-accordion-group>
      <br>
      <h1 class="ion-padding">📈 KPIs Técnicos</h1>
      <ion-accordion-group expand="inset" :multiple="true">
        <ion-accordion v-for="item in smartGoalsTecnico" :key="item.id" :value="item.id.toString()">
          <ion-item slot="header">
            <ion-label>{{ item.id }}. {{ item.title }}</ion-label>
          </ion-item>
          <div class="ion-padding" slot="content">
            <p>{{ item.description }}</p>
            <ion-list :inset="true">
              <ion-item v-for="(element, index) in item.smart" :key="index">
                <ion-label><b>{{ element.letter }}</b> → {{ element.content }}</ion-label>
              </ion-item>
            </ion-list>
          </div>
        </ion-accordion>
      </ion-accordion-group>
    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar, IonAccordionGroup, IonAccordion, IonItem, IonLabel, IonList } from '@ionic/vue';
import { ref } from 'vue';


// Definición de la estructura de datos para un objetivo SMART
interface SmartElement {
  letter: string;
  content: string;
}


interface SmartGoal {
  id: number;
  title: string;
  description: string;
  smart: SmartElement[];
}


// Array de objetivos SMART
const smartGoalsBusiness = ref<SmartGoal[]>([
  {
    id: 1,
    title: "Incrementar pedidos",
    description: "Incrementar los pedidos mensuales un 25% durante los próximos 3 meses mediante campañas de descuentos segmentadas.",
    smart: [
      { letter: "S", content: "Incrementar los pedidos mensuales" },
      { letter: "M", content: "25% (de 3,500 a 4,375)" },
      { letter: "A", content: "aplicando campañas de descuentos segmentadas" },
      { letter: "R", content: "para aumentar las ventas durante el primer semestre" },
      { letter: "T", content: "en los proximos 3 meses" }
    ]
  },
  {
    id: 2,
    title: "Aumentar usuarios",
    description: "Aumentar el número de usuarios registrados de 14,000 a 20,000 antes de finalizar el próximo trimestre impulsando campañas de adquisición digital.",
    smart: [
      { letter: "S", content: "Aumentar los usuarios registrados" },
      { letter: "M", content: "de 14,000 a 20,000" },
      { letter: "A", content: "mediante campañas de adquisición digital" },
      { letter: "R", content: "para expandir la base de clientes activos" },
      { letter: "T", content: "antes de finalizar el próximo trimestre" }
    ]
  },
  {
    id: 3,
    title: "Elevar la tasa de repeticion de clientes",
    description: "Elevar la tasa de repetición de clientes del 33% al 45% en los siguientes 4 meses mediante un sistema de recompensas y envíos gratuitos.",
    smart: [
      { letter: "S", content: "Incrementar la tasa de repetición" },
      { letter: "M", content: "del 33% al 45%" },
      { letter: "A", content: "implementando un sistema de recompensas y envíos gratuitos" },
      { letter: "R", content: "para mejorar la retención y aumentar el valor de cliente" },
      { letter: "T", content: "en los próximos 4 meses" }
    ]
  },
  {
    id: 4,
    title: "Asociarnos a mas restaurantes",
    description: "Aumentar el número de restaurantes asociados de 87 a 120 en los próximos 6 meses mediante acciones comerciales y acuerdos preferenciales.",
    smart: [
      { letter: "S", content: "Aumentar restaurantes asociados" },
      { letter: "M", content: "de 87 a 120" },
      { letter: "A", content: "mediante acuerdos preferenciales y acciones comerciales" },
      { letter: "R", content: "para ampliar la oferta y mejorar el servicio en más zonas" },
      { letter: "T", content: "en 6 meses" }
    ]
  },
  {
    id: 5,
    title: "Incrementar ingresos",
    description: "Incrementar los ingresos mensuales en un 20% durante los próximos 3 meses introduciendo promociones de combos y menú del día.",
    smart: [
      { letter: "S", content: "Incrementar ingresos mensuales" },
      { letter: "M", content: "20% (42,000 → 50,400 €)" },
      { letter: "A", content: "introduciendo promociones de combos y menú del día" },
      { letter: "R", content: "para aumentar las ventas y mejorar el ticket promedio" },
      { letter: "T", content: "en 3 meses" }
    ]
  }
]);

const smartGoalsTecnico = ref<SmartGoal[]>([
  {
    id: 1,
    title: "Aumentar el soporte de usuarios",
    description: "Aumentar la capacidad del sistema para soportar picos de usuarios de 5,000 a 10,000 usuarios simultáneos en los próximos 3 meses mediante mejoras en el escalado automático.",
    smart: [
      { letter: "S", content: "Aumentar la capacidad de usuarios simultáneos" },
      { letter: "M", content: "de 5,000 a 10,000" },
      { letter: "A", content: "mediante mejoras en el autoscaling del backend" },
      { letter: "R", content: "para evitar caídas o ralentizaciones durante picos de actividad" },
      { letter: "T", content: "en los próximos 3 meses" }
    ]
  },
  {
    id: 2,
    title: "Mejorar estabilidad",
    description: "Mejorar la estabilidad del sistema elevando el uptime del 99% al 99.6% durante los próximos 3 meses mediante redundancia y monitoreo avanzado.",
    smart: [
      { letter: "S", content: "Mejorar uptime" },
      { letter: "M", content: "99% → 99.6%" },
      { letter: "A", content: "añadiendo redundancia y monitoreo" },
      { letter: "R", content: "garantizar disponibilidad constante del servicio" },
      { letter: "T", content: "en 3 meses" }
    ]
  },
  {
    id: 3,
    title: "Disminuir tasa de errores",
    description: "Disminuir la tasa de errores de 8 a menos de 3 por cada 1,000 peticiones en un periodo de 8 semanas mediante pruebas automatizadas y despliegues escalonados.",
    smart: [
      { letter: "S", content: "Reducir errores" },
      { letter: "M", content: "de 8 a < 3 por 1,000" },
      { letter: "A", content: "aplicando pruebas automatizadas y despliegues escalonados" },
      { letter: "R", content: "mejorar la estabilidad y la experiencia del usuario" },
      { letter: "T", content: "en 8 semanas" }
    ]
  },
  {
    id: 4,
    title: "Reducir el consumo de CPU",
    description: "Reducir el consumo de CPU aproximadamente a un 45% en los próximos 45 días mediante optimización de procesos y actualización de servidores.",
    smart: [
      { letter: "S", content: "Reducir consumo de CPU" },
      { letter: "M", content: "a un ~45%" },
      { letter: "A", content: "optimizando procesos y actualizando infraestructura" },
      { letter: "R", content: "evitar saturaciones en horas pico" },
      { letter: "T", content: "en 45 días" }
    ]
  },
  {
    id: 5,
    title: "Reducir uso de RAM",
    description: "Reducir el uso mensual promedio de RAM de un 64% a un 55% en 2 meses mediante optimización de procesos internos y limpieza de sesiones inactivas.",
    smart: [
      { letter: "S", content: "Reducir el uso mensual de RAM" },
      { letter: "M", content: "de 64% a 55%" },
      { letter: "A", content: "optimizando procesos y eliminando sesiones inactivas" },
      { letter: "R", content: "para mejorar la eficiencia del sistema y evitar sobrecargas" },
      { letter: "T", content: "en 2 meses" }
    ]
  }
]);


</script>


<style scoped>


ion-accordion.accordion-collapsing ion-item[slot='header'],
  ion-accordion.accordion-collapsed ion-item[slot='header'] {
    --background: var(--ion-color-light);
    --color: var(--ion-color-light-contrast);
  }


  ion-accordion.accordion-expanding ion-item[slot='header'],
  ion-accordion.accordion-expanded ion-item[slot='header'] {
    --background: rgba(var(--ion-color-primary-rgb), 0.14);
    color: var(--ion-color-primary);
  }


</style>


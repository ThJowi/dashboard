<template>

  <div class="chart-container">
    <apexchart
      width="100%"
      height="300"
      type="pie"
      :options="options"
      :series="series"
    ></apexchart>
  </div>
</template>


<script>

import { defineComponent } from 'vue';
import ApexCharts from 'vue3-apexcharts';

export default defineComponent({
  name: 'PieChart',
  components: {
    apexchart: ApexCharts
  },
  props: {
    series: {
      type: Array,
      required: true
    },
    labels: {
      type: Array,
      required: true
    }
  },
  computed: {
    options() {
      return {
        labels: this.labels,
        legend: {
          position: 'bottom'
        }
      };
    }
  }
});

</script>


<style scoped>

.chart-container {
  width: 100%;
}

</style>
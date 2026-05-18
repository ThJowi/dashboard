<template>

  <div class="chart-container">
    <canvas ref="chartCanvas"></canvas>
  </div>

</template>


<script>

import { Chart, registerables } from 'chart.js';
import { ref, onMounted, onUnmounted } from 'vue';

Chart.register(...registerables);

export default {
  name: 'BarChart',
  props: {
    chartData: {
      type: Object,
      required: true
    },
    options: {
      type: Object,
      default: () => ({})
    }
  },
  setup(props) {
    const chartCanvas = ref(null);
    let chartInstance = null;
    const renderChart = () => {
      if (chartInstance) {
        chartInstance.destroy();
      }
      if (chartCanvas.value) {
        chartInstance = new Chart(chartCanvas.value, {
          type: 'bar',
          data: props.chartData,
          options: {
            responsive: true,
            maintainAspectRatio: false,
            ...props.options
          }
        });
      }
    };
    onMounted(() => {
      renderChart();
    });
    onUnmounted(() => {
      if (chartInstance) {
        chartInstance.destroy();
      }
    });
    return {
      chartCanvas
    };
  }
};

</script>



<style scoped>

.chart-container {
  position: relative;
  height: 300px;
  width: 100%;
}

</style>
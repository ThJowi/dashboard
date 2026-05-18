<template>
  <div class="chart-container">
    <canvas ref="chartRef"></canvas>
  </div>
</template>
<script>
import { Chart, registerables } from 'chart.js';
import { onMounted, ref, onUnmounted } from 'vue';
Chart.register(...registerables);
export default {
  name: 'MixedChart',
  props: {
    labels: Array,
    orders: Array,
    repeatRate: Array
  },
  setup(props) {
    const chartRef = ref(null);
    let chart = null;
    const createChart = () => {
      chart = new Chart(chartRef.value, {
        data: {
          labels: props.labels,
          datasets: [
            {
              type: 'bar',
              label: 'Pedidos',
              data: props.orders,
              backgroundColor: 'rgba(75,192,192,0.5)',
              borderColor: 'rgba(75,192,192,1)',
              borderWidth: 1,
              yAxisID: 'y'
            },
            {
              type: 'line',
              label: 'Tasa de repetición (%)',
              data: props.repeatRate,
              borderColor: '#ff7043',
              borderWidth: 3,
              tension: 0.3,
              yAxisID: 'y1'
            }
          ]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            y: {
              beginAtZero: true,
              position: 'left',
              title: { display: true, text: 'Pedidos' }
            },
            y1: {
              beginAtZero: true,
              position: 'right',
              grid: { drawOnChartArea: false },
              title: { display: true, text: 'Repetición (%)' }
            }
          }
        }
      });
    };
    onMounted(createChart);
    onUnmounted(() => chart && chart.destroy());
    return { chartRef };
  }
};
</script>
<style scoped>
.chart-container {
  width: 100%;
  height: 300px;
}
</style>
<template>

  <div class="chart-container">
    <canvas ref="canvasRef"></canvas>
  </div>

</template>


<script>

import { Chart, registerables } from 'chart.js';
import { ref, onMounted, onUnmounted } from 'vue';

Chart.register(...registerables);

export default {
  name: 'RTLineChart',
  props: {
    interval: {
      type: Number,
      default: 1000
    }
  },
  setup(props) {
    const canvasRef = ref(null);
    let chart = null;
    let timer = null;
    const initChart = () => {
      chart = new Chart(canvasRef.value, {
        type: 'line',
        data: {
          labels: [],
          datasets: [
            {
              label: 'Usuarios en tiempo real',
              data: [],
              borderColor: 'rgba(75,192,192,1)',
              backgroundColor: 'rgba(75,192,192,0.2)',
              borderWidth: 2,
              tension: 0.3
            }
          ]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          animation: false,
          scales: {
            x: { display: false },
            y: { beginAtZero: true }
          }
        }
      });
    };
    const startUpdates = () => {
      timer = setInterval(() => {
        const newValue = Math.floor(Math.random() * 300 + 200); 
        const timeLabel = new Date().toLocaleTimeString();
        chart.data.labels.push(timeLabel);
        chart.data.datasets[0].data.push(newValue);
        if (chart.data.labels.length > 20) {
          chart.data.labels.shift();
          chart.data.datasets[0].data.shift();
        }
        chart.update();
      }, props.interval);
    };
    onMounted(() => {
      initChart();
      startUpdates();
    });
    onUnmounted(() => {
      if (timer) clearInterval(timer);
      if (chart) chart.destroy();
    });
    return { canvasRef };
  }
};

</script>


<style scoped>

.chart-container {
  width: 100%;
  height: 300px;
}

</style>
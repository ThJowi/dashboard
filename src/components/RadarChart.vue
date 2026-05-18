<template>

  <div class="chart-container">
    <canvas ref="canvasRef"></canvas>
  </div>

</template>


<script>

import { Chart, registerables } from 'chart.js';
import { ref, onMounted, onUnmounted, watch } from 'vue';

Chart.register(...registerables);

export default {
  name: 'RadarChart',
  props: {
    labels: {
      type: Array,
      required: true 
    },
    dataValues: {
      type: Array,
      required: true 
    },
    etiqueta: {
      type: String,
      default: 'Indicadores'
    },
    maxScale: {
      type: Number,
      default: 100 
    }
  },
  setup(props) {
    const canvasRef = ref(null);
    let chart = null;
    const makeChart = () => {
      if (chart) chart.destroy();
      chart = new Chart(canvasRef.value, {
        type: 'radar',
        data: {
          labels: props.labels,
          datasets: [
            {
              label: props.etiqueta,
              data: props.dataValues,
              borderColor: 'rgba(75,192,192,1)',
              backgroundColor: 'rgba(75,192,192,0.2)',
              pointBackgroundColor: 'rgba(75,192,192,1)',
              pointRadius: 3,
              borderWidth: 2
            }
          ]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          animation: false,
          plugins: {
            legend: { display: true }
          },
          scales: {
            r: {
              suggestedMin: 0,
              suggestedMax: props.maxScale,
              ticks: {
                stepSize: Math.max(1, Math.round(props.maxScale / 5))
              },
              grid: { color: 'rgba(128,128,128,0.2)' },
              angleLines: { color: 'rgba(128,128,128,0.2)' },
              pointLabels: { font: { size: 12 } }
            }
          }
        }
      });
    };
    watch(
      () => [props.labels, props.dataValues, props.etiqueta, props.maxScale],
      () => {
        if (!chart) return;
        chart.data.labels = props.labels;
        chart.data.datasets[0].label = props.etiqueta;
        chart.data.datasets[0].data = props.dataValues;
        chart.options.scales.r.suggestedMax = props.maxScale;
        chart.update();
      },
      { deep: true }
    );
    onMounted(makeChart);
    onUnmounted(() => chart && chart.destroy());
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
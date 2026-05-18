<template>

  <div ref="chartRef" class="echart-container"></div>

</template>


<script>

import * as echarts from 'echarts';
import { onMounted, onUnmounted, ref } from 'vue';

export default {
  name: 'LineChart',
  props: {
    labels: {
      type: Array,
      required: true
    },
    values: {
      type: Array,
      required: true
    }
  },
  setup(props) {
    const chartRef = ref(null);
    let chartInstance = null;
    const initChart = () => {
        chartInstance = echarts.init(chartRef.value);
        const options = {
            tooltip: { trigger: 'axis' },
            xAxis: {
                type: 'category',
                data: props.labels
            },
            yAxis: { type: 'value' },
            series: [
                {
                    data: props.values,
                    type: 'line',
                    smooth: true
                }
            ]
        };
      chartInstance.setOption(options);
    };
    onMounted(() => {
        setTimeout(() => {
            initChart();
            window.addEventListener('resize', () => chartInstance.resize());
        }, 50);
    });
    onUnmounted(() => {
      if (chartInstance) chartInstance.dispose();
    });
    return { chartRef };
  }
};

</script>


<style scoped>

.echart-container {
  width: 100%;
  height: 300px;
}

</style>
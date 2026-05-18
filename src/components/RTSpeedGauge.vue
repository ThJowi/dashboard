<template>

  <div ref="chartRef" class="gauge-container"></div>

</template>


<script>

import * as echarts from 'echarts';
import { onMounted, onUnmounted, ref } from 'vue';

export default {
  name: 'RTSpeedGauge',
  props: {
    interval: {
      type: Number,
      default: 1000
    }
  },
  setup(props) {
    const chartRef = ref(null);
    let chart = null;
    let timer = null;
    const initChart = () => {
      chart = echarts.init(chartRef.value);
      const options = {
        series: [
          {
            type: 'gauge',
            startAngle: 210,
            endAngle: -30,
            min: 0,
            max: 100,
            splitNumber: 10,
            itemStyle: {
              color: '#4fc3f7',
            },
            progress: {
              show: true,
              width: 20
            },
            axisLine: {
              lineStyle: {
                width: 20
              }
            },
            pointer: {
              icon: 'rect',
              width: 6,
              length: '60%',
              itemStyle: {
                color: '#455a64'
              }
            },
            axisTick: {
              distance: -30,
              length: 8,
              lineStyle: {
                color: '#455a64',
                width: 2
              }
            },
            splitLine: {
              distance: -30,
              length: 30,
              lineStyle: {
                color: '#455a64',
                width: 3
              }
            },
            axisLabel: {
              distance: -45,
              color: '#455a64',
              fontSize: 12
            },
            detail: {
              fontSize: 24,
              color: '#455a64',
              formatter: '{value}%',
              offsetCenter: [0, '40%']
            },
            data: [
              {
                value: 0
              }
            ]
          }
        ]
      };
      chart.setOption(options);
    };
    const startUpdates = () => {
      timer = setInterval(() => {
        const newValue = Math.floor(Math.random() * 15 + 65); 
        chart.setOption({
          series: [
            {
              data: [{ value: newValue }]
            }
          ]
        });
      }, props.interval);
    };
    onMounted(() => {
      setTimeout(() => {
        initChart();
        startUpdates();
        setTimeout(() => {
          chart && chart.resize();
        }, 20);
        window.addEventListener('resize', () => chart && chart.resize());
      }, 50);
    });
    onUnmounted(() => {
      if (timer) clearInterval(timer);
      if (chart) chart.dispose();
    });
    return { chartRef };
  }
};

</script>


<style scoped>

.gauge-container {
  width: 100%;
  height: 300px;
}

</style>
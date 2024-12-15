<template>
  <div>
    <LineChart :data="chartData" :options="chartOptions" />
  </div>
</template>

<script setup>
import {
  CategoryScale,
  Chart as ChartJS,
  Legend,
  LinearScale,
  LineElement,
  PointElement,
  Title,
  Tooltip
} from 'chart.js';
import { ref } from 'vue';
import { Line } from 'vue-chartjs';

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement
);

const LineChart = Line;
const isChartReady = ref(false);
const chartData = {
  labels: [
    'Янв',
    'Фев',
    'Мар',
    'Апр',
    'Май',
    'Июн',
    'Июл',
    'Авг',
    'Сен',
    'Окт',
    'Ноя',
    'Дек'
  ],
  datasets: [
    {
      label: 'Продажи',
      data: [500, 700, 800, 600, 750, 900, 850, 950, 1000, 1100, 1050, 1150],
      borderColor: 'rgba(75, 192, 192, 1)',
      backgroundColor: 'rgba(75, 192, 192, 0.2)',
      tension: 0.4
    }
  ]
};
const chartOptions = {
  responsive: true,
  plugins: {
    legend: {
      position: 'top'
    },
    title: {
      display: true,
      text: 'Продажи за Месяц'
    }
  }
};
</script>

<style scoped>
/* Добавьте стили по необходимости */
</style>

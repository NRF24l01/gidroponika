<template>
  <!-- Graph 1 -->
  <div class="bg-gray-800 p-4 rounded-lg">
    <div class="flex justify-between items-center mb-4">
      <h2 class="text-lg font-semibold">24h</h2>
      <button class="bg-gray-700 px-3 py-1 rounded-lg hover:bg-gray-600">
        Свой диапазон
      </button>
    </div>
    <Line :data="waterChartData" :options="chartOptions" class="h-48" />
    <p class="text-center text-gray-400 mt-2">Вода °C</p>
  </div>

  <!-- Graph 2 -->
  <Plot
    :series="series"
    :categories="categories"
    :baseOptions="baseOptions"
    :presets="['24h', '12h', '6h']"
  />
</template>

<script setup>
import Plot from "@/components/Plot.vue"

const categories = Array.from({ length: 24 }, (_, i) =>
  `${String(i).padStart(2, '0')}:00`
)

const generateData = (base, variance) =>
  Array.from({ length: 24 }, () =>
    +(base + Math.random() * variance * 2 - variance).toFixed(1)
  )

const series = [
  {
    name: 'Температура воды',
    data: generateData(24, 1.5),
    color: '#0ea5e9'
  },
  {
    name: 'Температура воздуха',
    data: generateData(21, 2.5),
    color: '#8b5cf6'
  },
  {
    name: 'Температура почвы',
    data: generateData(18, 1),
    color: '#16a34a'
  }
]

const baseOptions = {
  yaxis: {
    title: { text: 'Температура (°C)' }
  },
  legend: { show: true }
}

import { ref } from "vue";
import { Line } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
  Filler,
} from "chart.js";

// Register Chart.js components
ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
  Filler
);

// Example data for the graphs
const waterChartData = {
  labels: ["00:00", "06:00", "12:00", "18:00", "24:00"],
  datasets: [
    {
      label: "Вода °C",
      data: [22, 23, 24, 23, 22],
      borderColor: "#3b82f6",
      backgroundColor: "rgba(59, 130, 246, 0.2)",
      fill: true,
    },
  ],
};

const airChartData = {
  labels: ["00:00", "06:00", "12:00", "18:00", "24:00"],
  datasets: [
    {
      label: "Воздух °C",
      data: [25, 21, 22, 21, 20],
      borderColor: "#f97316",
      backgroundColor: "rgba(249, 115, 22, 0.2)",
      fill: true,
    },
  ],
};

const chartOptions = {
  responsive: true,
  plugins: {
    legend: { display: false },
  },
};
</script>

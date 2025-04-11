<script setup>
import { ref } from 'vue'
import { Line } from 'vue-chartjs'
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
} from 'chart.js'

import {
  CalendarIcon,
  WrenchIcon,
  ChartBarIcon
} from "@heroicons/vue/24/outline"

// Register Chart.js components
ChartJS.register(Title, Tooltip, Legend, LineElement, CategoryScale, LinearScale, PointElement, Filler)

// Example data for the graphs
const waterChartData = {
  labels: ['00:00', '06:00', '12:00', '18:00', '24:00'],
  datasets: [
    {
      label: 'Вода °C',
      data: [22, 23, 24, 23, 22],
      borderColor: '#3b82f6',
      backgroundColor: 'rgba(59, 130, 246, 0.2)',
      fill: true,
    },
  ],
}

const airChartData = {
  labels: ['00:00', '06:00', '12:00', '18:00', '24:00'],
  datasets: [
    {
      label: 'Воздух °C',
      data: [25, 21, 22, 21, 20],
      borderColor: '#f97316',
      backgroundColor: 'rgba(249, 115, 22, 0.2)',
      fill: true,
    },
  ],
}

const chartOptions = {
  responsive: true,
  plugins: {
    legend: { display: false },
  },
}
</script>

<template>
  <main class="bg-gray-900 text-white min-h-screen p-6">
    <!-- Header -->
    <header class="flex justify-between items-center mb-6">
      <h1 class="text-xl font-bold flex items-center space-x-2">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-blue-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h11M9 21V3m12 7h-3m0 0l-3 3m3-3l3 3" />
        </svg>
        <span>Система управления освещением</span>
      </h1>
      <button class="bg-gray-800 px-4 py-2 rounded-lg hover:bg-gray-700 flex items-center space-x-2">
        <WrenchIcon class="size-6 text-white" />
        <span>Термометры</span>
      </button>
    </header>

    <!-- Subheader -->
    <p class="text-gray-400 mb-4">
      Мониторинг температуры и настройка расписания освещения
    </p>

    <!-- Tabs -->
    <div class="flex space-x-4 mb-6">
      <button class="bg-gray-800 px-4 py-2 rounded-lg hover:bg-gray-700 flex items-center space-x-2">
        <ChartBarIcon class="size-6 text-white" />
        <span>Статистика</span>
      </button>
      <button class="bg-gray-800 px-4 py-2 rounded-lg hover:bg-gray-700 flex items-center space-x-2">
        <CalendarIcon class="size-6 text-white" />
        <span>Расписание</span>
      </button>
    </div>

    <!-- Graphs Section -->
    <section class="grid grid-cols-1 md:grid-cols-2 gap-6">
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
      <div class="bg-gray-800 p-4 rounded-lg">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-lg font-semibold">24h</h2>
          <button class="bg-gray-700 px-3 py-1 rounded-lg hover:bg-gray-600">
            Свой диапазон
          </button>
        </div>
        <Line :data="airChartData" :options="chartOptions" class="h-48" />
        <p class="text-center text-gray-400 mt-2">Воздух °C</p>
      </div>
    </section>

    <!-- Footer -->
    <footer class="text-center text-gray-500 mt-6">
      © 2025 Ambient Glow Scheduler
    </footer>
  </main>
</template>
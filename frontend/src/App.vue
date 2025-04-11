<script setup>
import {
  CalendarIcon,
  WrenchIcon,
  ChartBarIcon,
  HomeIcon
} from "@heroicons/vue/24/outline"

import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <main class="bg-gray-900 text-white min-h-screen p-6 font-sans">
    <!-- Header -->
    <header class="flex justify-between items-center mb-6">
      <h1 class="text-xl font-bold flex items-center space-x-2">
        <HomeIcon class="size-7 text-blue-500" />
        <span>Система управления грядкой</span>
      </h1>
      <button class="bg-gray-800 px-4 py-2 rounded-lg hover:bg-gray-700 flex items-center space-x-2">
        <WrenchIcon class="size-6 text-white" />
        <span>Термометры</span>
      </button>
    </header>

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

    <!-- Section -->
    <section class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <RouterView />
    </section>

    <!-- Footer -->
    <footer class="text-center text-gray-500 mt-6">
      © 2025 Ambient Glow Scheduler
    </footer>
  </main>
</template>

<style scoped>
</style>

<template>
  <div class="flex items-center bg-gray-800 rounded-lg mx-2">
    <button
      :class="{
        'bg-gray-700 text-white': $route.path === '/stats',
        'text-gray-400': $route.path !== '/stats',
      }"
      @click="$router.push('/stats')"
      class="flex flex-1 justify-center py-2 px-4 rounded-lg focus:outline-none transitio items-center"
    >
      <ChartPieIcon class="size-6 mr-1" /> Температура
    </button>
    <button
      :class="{
        'bg-gray-700 text-white': $route.path === '/shedule',
        'text-gray-400': $route.path !== '/shedule',
      }"
      @click="$router.push('/shedule')"
      class="flex flex-1 justify-center py-2 px-4 rounded-lg focus:outline-none transition items-center"
    >
      <CalendarIcon class="size-6 mr-1" />Расписание
    </button>
  </div>
</template>

<script setup>
import {
  CalendarIcon,
  ChartPieIcon
} from "@heroicons/vue/24/outline"
</script>

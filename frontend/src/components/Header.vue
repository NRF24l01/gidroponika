<template>
  <!-- Header -->
  <header class="flex justify-between items-center mb-6 p-6 bg-gray-800">
    <h1 class="text-xl font-bold flex items-center space-x-2">
      <HomeIcon class="size-7 text-blue-500" />
      <span>Система управления грядкой</span>
    </h1>
    <div>
      <RouterLink to="/temp" class="bg-gray-800 px-6 py-5">
        <span>Температура</span>
      </RouterLink>
      <RouterLink to="/light" class="bg-gray-800 px-6 py-5">
        <span>Освещение</span>
      </RouterLink>
      <RouterLink to="/term" class="bg-gray-800 px-6 py-5">
        <span>Термометры</span>
      </RouterLink>
    </div>
  </header>
</template>


<script setup>
import {
  HomeIcon
} from "@heroicons/vue/24/outline"
</script>
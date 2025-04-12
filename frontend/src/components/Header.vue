<template>
  <!-- Header -->
  <header class="flex justify-between items-center mb-6 p-4 bg-gray-800">
    <h1 class="text-xl font-bold flex items-center space-x-2">
      <HomeIcon class="size-7 text-blue-500" />
      <span>Система управления грядкой</span>
    </h1>
    <button class="bg-gray-800 px-4 py-2 rounded-lg hover:bg-gray-700 flex items-center space-x-2">
      <WrenchIcon class="size-6 text-white" />
      <span>Термометры</span>
    </button>
  </header>
</template>


<script setup>
import {
  WrenchIcon,
  HomeIcon
} from "@heroicons/vue/24/outline"
</script>
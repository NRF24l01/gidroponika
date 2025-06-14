<template>
  <!-- Header -->
  <header class="flex justify-between items-center mb-3 p-4 bg-gray-800 relative text-white">
    <h1 class="text-xl font-bold flex items-center space-x-2">
      <HomeIcon class="size-7 text-blue-500" />
      <span>Система управления грядкой</span>
    </h1>
    <!-- Desktop menu -->
    <div class="hidden md:flex space-x-2">
      <RouterLink to="/temp" class="px-6 py-5">
        <span>Температура</span>
      </RouterLink>
      <RouterLink to="/light" class="px-6 py-5">
        <span>Освещение</span>
      </RouterLink>
      <RouterLink to="/term" class="px-6 py-5">
        <span>Термометры</span>
      </RouterLink>
    </div>
    <!-- Burger button (mobile) -->
    <button
      class="md:hidden flex items-center px-3 py-2 border rounded text-gray-200 border-gray-400"
      @click="menuOpen = !menuOpen"
      aria-label="Открыть меню"
    >
      <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
          d="M4 6h16M4 12h16M4 18h16"/>
      </svg>
    </button>
    <!-- Mobile menu -->
    <transition name="fade">
      <div
        v-if="menuOpen"
        class="absolute top-full right-0 mt-2 w-48 bg-gray-800 rounded shadow-lg flex flex-col z-50 md:hidden"
      >
        <RouterLink
          to="/temp"
          class="px-6 py-4 hover:bg-gray-700 border-b border-gray-700"
          @click="menuOpen = false"
        >
          Температура
        </RouterLink>
        <RouterLink
          to="/light"
          class="px-6 py-4 hover:bg-gray-700 border-b border-gray-700"
          @click="menuOpen = false"
        >
          Освещение
        </RouterLink>
        <RouterLink
          to="/term"
          class="px-6 py-4 hover:bg-gray-700"
          @click="menuOpen = false"
        >
          Термометры
        </RouterLink>
      </div>
    </transition>
  </header>
</template>

<script setup>
import { ref } from "vue"
import { HomeIcon } from "@heroicons/vue/24/outline"

const menuOpen = ref(false)
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
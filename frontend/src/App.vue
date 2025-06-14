<script setup>
import { RouterLink, RouterView } from 'vue-router'

import Header from "@/components/Header.vue"
import Footer from "@/components/Footer.vue"
</script>

<template>
  <div class="min-h-screen flex flex-col bg-gray-100 text-gray-900 font-sans">
    <Header />
    
    <!-- Контент заполняет доступное пространство -->
    <main class="flex-grow flex justify-center px-4 py-6">
      <section class="w-full max-w-6xl grid gap-6">
      <RouterView />
      </section>
    </main>

    <!-- Футер выходит за пределы -->
    <div class="relative">
      <Footer />
    </div>
  </div>
</template>

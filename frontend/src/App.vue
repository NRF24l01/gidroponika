<script setup>
import { RouterLink, RouterView } from 'vue-router'

import Header from "@/components/Header.vue"
import Tabs from "@/components/Tabs.vue"
import Footer from "@/components/Footer.vue"
</script>

<template>
  <div class="min-h-screen flex flex-col bg-gray-900 text-white font-sans">
    <Header />
    <Tabs />
    
    <!-- Контент заполняет доступное пространство -->
    <main class="flex-grow p-6">
      <section class="grid gap-6">
        <RouterView />
      </section>
    </main>

    <!-- Футер выходит за пределы -->
    <div class="relative">
      <Footer />
    </div>
  </div>
</template>

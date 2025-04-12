<template>
  <div class="flex items-center bg-gray-800 py-1 px-4 rounded-lg w-full mx-auto">
    <button
      :class="{
        'bg-gray-700 text-white': selected === 'temperature',
        'text-gray-400': selected !== 'temperature',
      }"
      @click="selected = 'temperature'"
      class="flex-1 py-2 px-4 rounded-lg focus:outline-none transition"
    >
      <span class="mr-2">🌡️</span>Температура
    </button>
    <button
      :class="{
        'bg-gray-700 text-white': selected === 'schedule',
        'text-gray-400': selected !== 'schedule',
      }"
      @click="selected = 'schedule'"
      class="flex-1 py-2 px-4 rounded-lg focus:outline-none transition"
    >
      <span class="mr-2">📅</span>Расписание
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selected: "temperature",
    };
  },
};
</script>

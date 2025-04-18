<script setup>
import { ref, computed } from 'vue'
import ApexChart from 'vue3-apexcharts'

const props = defineProps({
  series: {
    type: Array,
    required: true
  },
  categories: {
    type: Array,
    required: true
  },
  baseOptions: {
    type: Object,
    default: () => ({})
  },
  presets: {
    type: Array,
    default: () => ['24h', '12h', '6h', '1h']
  }
})

const timeRange = ref(props.presets[0])

const filteredSeries = computed(() => {
  const hours = parseInt(timeRange.value.replace('h', ''))
  return props.series.map((s) => ({
    ...s,
    data: s.data.slice(-hours)
  }))
})

const filteredCategories = computed(() => {
  const hours = parseInt(timeRange.value.replace('h', ''))
  return props.categories.slice(-hours)
})

const mergedOptions = computed(() => ({
  chart: {
    type: 'line',
    toolbar: { show: false }
  },
  stroke: { curve: 'smooth', width: 3 },
  markers: { size: 4 },
  xaxis: { categories: filteredCategories.value },
  colors: props.series.map(s => s.color || '#8884d8'),
  tooltip: {
    theme: 'dark',
    x: { format: 'HH:mm' }
  },
  ...props.baseOptions
}))
</script>

<template>
  <div class="w-full bg-gray-800 rou">
    <div class="flex gap-2 mb-4" v-if="presets.length">
      <button
        v-for="preset in presets"
        :key="preset"
        @click="timeRange = preset"
        class="px-3 py-1 rounded-lg border"
        :class="preset === timeRange ? 'bg-blue-600 text-white' : 'bg-white text-black'"
      >
        {{ preset }}
      </button>
    </div>

    <apexchart
      width="100%"
      height="300"
      type="line"
      :options="mergedOptions"
      :series="filteredSeries"
    />
  </div>
</template>

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
  xaxis: { 
    categories: filteredCategories.value,
    labels: { style: { colors: '#FFFFFF' } } // Set x-axis labels to white
  },
  yaxis: { 
    labels: { style: { colors: '#FFFFFF' } } // Set y-axis labels to white
  },
  legend: {
    labels: { colors: '#FFFFFF' }, // Set legend text color to white
    fontSize: '12px', // Optional: Adjust font size if needed
    fontFamily: 'Helvetica, Arial, sans-serif' // Optional: Ensure consistent font
  },
  colors: props.series.map(s => s.color || '#8884d8'),
  tooltip: {
    theme: 'dark',
    x: { format: 'HH:mm' }
  },
  ...props.baseOptions
}))
</script>

<template>
  <div class="w-full bg-gray-800 rou rounded-xl px-1">
    <apexchart
      width="100%"
      height="300"
      type="line"
      :options="mergedOptions"
      :series="filteredSeries"
      class="text-white"
    />
  </div>
</template>

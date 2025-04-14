<template>
  <div class="rounded-2xl p-4 bg-gray-900 text-white">
    <div class="flex justify-between items-center mb-4 flex-wrap gap-2">
      <div v-if="customMode" class="flex gap-2 items-end">
        <div>
          <label class="block text-sm mb-1">С</label>
          <input
            type="time"
            v-model="startTime"
            class="rounded-md p-1 text-black"
          />
        </div>
        <div>
          <label class="block text-sm mb-1">По</label>
          <input
            type="time"
            v-model="endTime"
            class="rounded-md p-1 text-black"
          />
        </div>
        <button
          @click="toggleCustomMode"
          class="ml-2 p-2 bg-gray-700 rounded-md"
        >
          ⇄
        </button>
      </div>
      <div v-else class="flex items-center gap-2">
        <div class="grid grid-cols-4 gap-2">
          <button
            v-for="range in presets"
            :key="range"
            :class="[
              'px-3 py-1 rounded-md',
              timeRange === range ? 'bg-blue-600' : 'bg-gray-700',
            ]"
            @click="timeRange = range"
          >
            {{ range }}
          </button>
        </div>
        <button
          @click="toggleCustomMode"
          class="ml-4 p-2 bg-gray-700 rounded-md flex items-center gap-1"
        >
          <span class="material-icons">calendar_today</span>
          <span class="hidden sm:inline">Свой диапазон</span>
        </button>
      </div>
    </div>

    <apexchart
      width="100%"
      height="280"
      type="line"
      :options="mergedOptions"
      :series="filteredSeries"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, computed, watch } from "vue";
import type { PropType } from "vue";
import ApexChart from "vue3-apexcharts";
import type { ApexOptions, ApexAxisChartSeries } from "apexcharts";

// === Props ===
const props = defineProps<{
  series: ApexAxisChartSeries;
  categories: string[];
  baseOptions?: ApexOptions;
  presets?: string[];
}>();

// === Time filtering state ===
const presets = props.presets ?? ["24h", "12h", "6h", "1h"];
const timeRange = ref(presets[0]);
const customMode = ref(false);
const startTime = ref("00:00");
const endTime = ref("23:59");

const toggleCustomMode = () => {
  customMode.value = !customMode.value;
};

// === Category filtering ===
const filteredCategories = computed(() => {
  const all = props.categories;
  if (customMode.value) {
    const [startH] = startTime.value.split(":").map(Number);
    const [endH] = endTime.value.split(":").map(Number);

    return all.filter((label) => {
      const hour = parseInt(label.split(":")[0]);
      return startH <= endH
        ? hour >= startH && hour <= endH
        : hour >= startH || hour <= endH;
    });
  } else {
    const limit = parseInt(timeRange.value.replace("h", ""));
    return all.slice(-limit);
  }
});

// === Filter series based on categories ===
const filteredSeries = computed(() => {
  return props.series.map((s) => ({
    ...s,
    data: props.categories.reduce<string[] | number[]>((acc, label, idx) => {
      if (filteredCategories.value.includes(label)) {
        acc.push(s.data[idx]);
      }
      return acc;
    }, []),
  }));
});

// === Merged chart options ===
const mergedOptions = computed<ApexOptions>(() => ({
  ...props.baseOptions,
  chart: {
    ...(props.baseOptions?.chart || {}),
    background: "transparent",
    toolbar: { show: false },
  },
  xaxis: {
    ...(props.baseOptions?.xaxis || {}),
    categories: filteredCategories.value,
    labels: { style: { colors: "#fff" } },
  },
  yaxis: {
    ...(props.baseOptions?.yaxis || {}),
    labels: { style: { colors: "#fff" } },
  },
  legend: {
    ...(props.baseOptions?.legend || {}),
    labels: { colors: "#fff" },
  },
  tooltip: {
    ...(props.baseOptions?.tooltip || {}),
    theme: "dark",
  },
  stroke: {
    ...(props.baseOptions?.stroke || {}),
    curve: "smooth",
    width: 3,
  },
}));
</script>

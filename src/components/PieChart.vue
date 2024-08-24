<script setup lang="ts">
import { Pie } from "vue-chartjs";
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from "chart.js";
import { onMounted, PropType, ref } from "vue";
import { ChartValue } from "@/data/chartData";
import { defineProps } from "vue";

ChartJS.register(ArcElement, Tooltip, Legend);
const props = defineProps({
  chartData: {
    type: Array as PropType<Array<ChartValue>>,
    required: true,
  },
  selectedCities: Array as PropType<Array<string>>,
});

const chartData = ref({
  labels: [],
  datasets: [
    {
      backgroundColor: [],
      data: [],
    },
  ],
});

const clearChart = () => {
  chartData.value.labels = [];
  chartData.value.datasets[0].data = [];
  chartData.value.datasets[0].backgroundColor = [];
};

const fillChart = () => {
  if (!props.selectedCities?.length) {
    for (let i = 0; i < props.chartData.length; i++) {
      chartData.value.labels.push(props.chartData[i].name);
      chartData.value.datasets[0].data.push(props.chartData[i].data);
      chartData.value.datasets[0].backgroundColor.push(
        stringToColour(props.chartData[i].name)
      );
    }
  } else {
    clearChart();
  }
};

const stringToColour = (str: string) => {
  let hash = 0;
  str.split("").forEach((char) => {
    hash = char.charCodeAt(0) + ((hash << 5) - hash);
  });
  let colour = "#";
  for (let i = 0; i < 3; i++) {
    const value = (hash >> (i * 8)) & 0xff;
    colour += value.toString(16).padStart(2, "0");
  }
  return colour;
};

onMounted(() => {
  fillChart();
});
</script>

<template>
  <Pie
    @click="() => console.log(1)"
    id="pie-id"
    :data="chartData"
    v-if="chartData.datasets[0].data.length > 0"
  />
</template>

<style scoped lang="scss"></style>

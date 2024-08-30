<script setup lang="ts">
import { Bar } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";
import { defineProps, PropType, reactive } from "vue";
import { ChartValue } from "@/data/chartData";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
);

const props = defineProps({
  chartData: {
    type: Array as PropType<Array<ChartValue>>,
    required: true,
  },
});

const chartData = reactive({
  labels: ["January", "February", "March", "April"],
  datasets: [
    {
      data: [40, 20, 12, 50],
      backgroundColor: ["#FF464F", "#FF8A34", "#FFBC25", "#25C685"],
    },
  ],
});
const chartOptions = reactive({
  responsive: true,
});
</script>

<template>
  <Bar id="my-chart-id" :options="chartOptions" :data="chartData" />
</template>

<style scoped lang="scss"></style>

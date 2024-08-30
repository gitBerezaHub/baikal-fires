<script setup lang="ts">
import { Pie } from "vue-chartjs";
import { ArcElement, Chart as ChartJS, Legend, Tooltip } from "chart.js";
import { defineProps, onMounted, PropType, reactive, watch } from "vue";
import { ChartValue } from "@/data/chartData";

ChartJS.register(ArcElement, Tooltip, Legend);
const props = defineProps({
  chartData: {
    type: Array as PropType<Array<ChartValue>>,
    required: true,
  },
});

const chartData = reactive({
  labels: [],
  datasets: [
    {
      data: [],
      backgroundColor: ["#FF464F", "#FF8A34", "#FFBC25", "#25C685"],
    },
  ],
});

const chartOptions = reactive({
  responsive: true,
  maintainAspectRatio: true,
  legend: { display: false },
});

const fillChart = () => {
  for (let i = 0; i < props.chartData.length; i++) {
    chartData.labels.push(props.chartData[i].name);
    chartData.datasets[0].data.push(props.chartData[i].data);
  }
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
    :options="chartOptions"
    v-if="chartData.datasets[0].data.length > 0"
  />
</template>

<style scoped lang="scss"></style>

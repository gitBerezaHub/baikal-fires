<script setup lang="ts">
import PieChart from "@/components/PieChart.vue";
import { defineProps, PropType } from "vue";
import { ChartValue } from "@/data/chartData";
import BarChart from "@/components/BarChart.vue";

const props = defineProps({
  chartData: {
    type: Array as PropType<Array<ChartValue>>,
    required: true,
  },
});
</script>

<template>
  <div class="wrapper">
    <div class="left-side">
      <BarChart :chart-data="props.chartData" />
    </div>
    <div class="right-side">
      <PieChart :chart-data="props.chartData" />
    </div>
  </div>
</template>

<style scoped lang="scss">
.wrapper {
  display: flex;
  flex-direction: row;
  width: 100vw;
  height: 100vh;
  border-top: 10px solid #000;
}

.left-side,
.right-side {
  width: 50%;
}
</style>

<template>
  <MainTitle />
  <CityChoice id="city-choice" :cityNameList="cityNameList" />
  <ChartPage id="chart-page" :chart-data="chartData" />
</template>

<script lang="ts" setup>
import { chartDataHardCode } from "@/data/chartData";
import CityChoice from "@/components/CityChoice.vue";
import MainTitle from "@/components/MainTitle.vue";
import { onMounted, ref } from "vue";
import ChartPage from "@/components/ChartPage.vue";

let chartData = chartDataHardCode;
const cityNameList = ref([]);
onMounted(() => {
  for (let i = 0; i < chartData.length; i++) {
    cityNameList.value.push(chartData[i].name);
  }
  cityNameList.value = cityNameList.value.sort();
});
</script>

<style lang="scss">
@import "styles/reset";

html {
  scroll-behavior: smooth;
  overflow-y: scroll;
}

#app {
  width: 100vw;
  height: 100vh;
  font-family: "Open Sans";
  background-size: cover;
  background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url("@/styles/background.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-attachment: fixed;
  padding-top: 150px;
}
</style>

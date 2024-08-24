<template>
  <div class="title">
    <h1 class="title-text">
      Бизнес Метрики <br />
      Пожары на Байкале
    </h1>
    <a href="#pieChart" class="show-statistic">Посмотреть статистику</a>
  </div>

  <main id="pieChart">
    <div class="left">
      <h1>Выбор городов</h1>
      <select v-model="selectedCities" multiple>
        <option v-for="city in allCities" :key="city" :value="city">
          {{ city }}
        </option>
      </select>
      <p v-if="!selectedCities.length">Показаны все города</p>
      <p v-else>Показаны города: {{ selectedCities.toString() }}</p>
    </div>
    <div class="right">
      <PieChart :chartData="chartData" :selectedCities="selectedCities" />
    </div>
  </main>
</template>

<script lang="ts" setup>
import PieChart from "@/components/PieChart.vue";
import { chartDataHardCode } from "@/data/chartData";
import { onMounted, ref } from "vue";

let chartData = chartDataHardCode;
const allCities = ref([]);
const selectedCities = ref([]);

onMounted(() => {
  for (let i = 0; i < chartData.length; i++) {
    allCities.value.push(chartData[i].name);
  }
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
    url("styles/background.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-attachment: fixed;
  padding-top: 150px;
}

.title {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
}

.title-text {
  text-align: center;
  color: #fff;
  font-size: 64px;
}

.show-statistic {
  text-decoration: none;
  color: #fff;
  font-size: 20px;
  border: 1px solid #fff;
  border-radius: 25px;
  padding: 15px;
  width: fit-content;
  margin-top: 50px;
}

#pieChart {
  margin-top: auto;
  height: 100vh;
  border-top: 1px solid #000;
  display: flex;
  flex-direction: row;

  .left,
  .right {
    width: 50vw;
    height: 100vh;
    display: flex;
    flex-direction: column;
  }

  .up,
  .down {
    width: 50vw;
    height: 50vh;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
}
</style>

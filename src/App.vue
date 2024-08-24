<template>
  <div class="title">
    <h1 class="title-text">
      Бизнес Метрики <br />
      Пожары на Байкале
    </h1>
    <a href="#down">Посмотреть статистику</a>
  </div>

  <main id="down">
    <div class="left">
      <table>
        <tr>
          <th>Название</th>
          <th>Количесто</th>
        </tr>
        <tr v-for="item in chartData.labels" :key="item">
          <th>{{ item }}</th>
          <th>
            {{ chartData.datasets[0].data[chartData.labels.indexOf(item)] }}
          </th>
        </tr>
      </table>
    </div>
    <div class="right">
      <Pie
        id="pie-id"
        :options="chartOptions"
        :data="chartData"
        v-if="chartData.datasets[0].data.length > 0"
      />
    </div>
  </main>
</template>

<script lang="ts" setup>
import { onMounted, ref } from "vue";
import { Pie } from "vue-chartjs";
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from "chart.js";
import { fireDataHardCode } from "@/data/fireData";

ChartJS.register(ArcElement, Tooltip, Legend);

let fireData = fireDataHardCode;
const chartData = ref({
  labels: [],
  datasets: [
    {
      backgroundColor: ["#41B883", "#E46651", "#00D8FF", "#DD1B16"],
      data: [],
    },
  ],
});
let chartOptions: {
  responsive: true;
  maintainAspectRatio: false;
  legend: {
    display: false;
  };
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
async function getFireCounts() {
  const url = "http://192.168.10.12:5280/metric/FireCounts";
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error("status: " + response.status);
    }
    const json = await response.json();
    console.log(json);
    fireData = json;
  } catch (error: any) {
    console.log(error.message);
  }
}
function fillChart() {
  for (let i = 0; i < fireData.length; i++) {
    chartData.value.labels.push(fireData[i].name);
    chartData.value.datasets[0].data.push(fireData[i].data);
    chartData.value.datasets[0].backgroundColor.push(
      stringToColour(fireData[i].name)
    );
  }
  console.log("1");
}

onMounted(() => {
  // getFireCounts();
  fillChart();
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

a {
  text-decoration: none;
  color: #fff;
  font-size: 20px;
  border: 1px solid #fff;
  border-radius: 25px;
  padding: 15px;
  width: fit-content;
  margin-top: 50px;
}

#down {
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

  .show-data {
    background-color: #fff;
    border: 1px solid #000;
    border-radius: 24px;
    padding: 10px;
    width: fit-content;
  }

  .show-data-text {
    color: #898787;
    font-size: 14px;
    margin-top: 10px;
  }
}
table,
th,
td {
  border: 1px solid black;
}
</style>

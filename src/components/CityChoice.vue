<script setup lang="ts">
import { PropType, ref } from "vue";
import { defineProps } from "vue";

const props = defineProps({
  cityNameList: {
    type: Array as PropType<Array<string>>,
    required: true,
  },
});

const chosenCities = ref([]);

const addOrRemoveCity = (city: string) => {
  if (!chosenCities.value.includes(city)) {
    chosenCities.value.push(city);
  } else {
    const index = chosenCities.value.indexOf(city);
    if (index > -1) {
      chosenCities.value.splice(index, 1);
    }
  }
};
</script>

<template>
  <div class="wrapper">
    <div class="title">
      <h1 class="header">Выберите Города</h1>
      <p class="sub-header">По которым хотите посмотреть статистику</p>
    </div>
    <div class="cityList">
      <button
        class="cityButton"
        :class="chosenCities.includes(city) && 'chosen-city'"
        v-for="city in props.cityNameList"
        :key="city"
        @click="addOrRemoveCity(city)"
      >
        {{ city }}
      </button>
    </div>
    <div class="footer" :class="!chosenCities.length && 'disabled-footer'">
      <button class="footer-button">Посмотреть</button>
      <img src="@/styles/down-arrow2.svg" alt="" width="60" />
    </div>
  </div>
</template>

<style scoped lang="scss">
.wrapper {
  border-top: 10px solid #000;
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  flex-direction: column;

  .title {
    margin-top: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;

    .header {
      font-size: 36px;
      margin-bottom: 5px;
    }
  }

  .cityList {
    margin-top: 30px;
    width: 75vw;
    height: fit-content;
    text-align: center;

    .cityButton {
      margin: 5px;
      font-size: 16px;
      background-color: #fff;
      border: 2px solid #000;
      border-radius: 10px;
      height: fit-content;
      width: fit-content;
      padding: 10px;
      transition: all 0.5s ease;
      cursor: pointer;

      &:hover {
        background-color: #56d9a4;
        border-color: #56d9a4;
      }
    }

    .chosen-city,
    .chosen-city:hover {
      border-color: #3dd598;
      background-color: #3dd598;
    }
  }

  .footer {
    display: flex;
    align-items: center;
    justify-content: space-around;
    margin-top: 20px;
    border: 2px solid #000;
    border-radius: 40px;
    padding: 10px 40px;
    transition: all 0.2s ease;
    cursor: pointer;

    .footer-button {
      background-color: transparent;
      border: none;
      font-size: 28px;
      margin-right: 20px;
      cursor: pointer;
    }
  }

  .disabled-footer {
    opacity: 0.3;
  }
}
</style>

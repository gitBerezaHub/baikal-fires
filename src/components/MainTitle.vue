<script setup lang="ts"></script>

<template>
  <div class="title">
    <h1 class="title-text">
      Бизнес Метрики <br />
      Пожары на Байкале
    </h1>
    <a href="#cityChoice" class="show-statistic">Посмотреть статистику</a>
  </div>
</template>

<style scoped lang="scss">
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
</style>

<script setup>
import { ref } from "vue";
import Carousel from "./components/Carousel.vue";
import PieChart from "./components/PieChart.vue";

const isViewVisible = ref(false);

const toggleView = () => {
  isViewVisible.value = !isViewVisible.value;
};
</script>

<template>
  <div class="my-2">
    <button @click="toggleView()" class="mx-3">Switch Component</button>
  </div>

  <div class="card">
    <Carousel v-if="isViewVisible" />
    <PieChart v-else />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>

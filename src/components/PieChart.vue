<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

let chart = null;

const newItem = ref();
const newLabel = ref();

const dataset = [300, 50, 100];

const data = {
  labels: ["Red", "Blue", "Yellow"],
  datasets: [
    {
      label: "Pie Chart",
      data: dataset,
      backgroundColor: [
        "rgb(255, 99, 132)",
        "rgb(54, 162, 235)",
        "rgb(255, 205, 86)",
      ],
      hoverOffset: 4,
    },
  ],
};

const config = {
  type: "pie",
  data: data,
};

function updateChart() {
  dataset.push(newItem.value);
  chart.data.datasets[0].data = dataset;
  chart.data.labels.push(newLabel.value);
  chart.data.datasets[0].backgroundColor.push(newLabel.value);
  chart.update();
}
onMounted(() => {
  const ctx = document.getElementById("chart");
  chart = new Chart(ctx, config);
});

onBeforeUnmount(() => {
  chart.destroy();
});
</script>

<template>
  <h3 class="my-3 font-bold text-2xl">Pie Chart</h3>
  <div class="w-[300px] h-[300px] mx-auto bg-gray-200">
    <canvas id="chart"></canvas>
  </div>
  <div>
    <input
      type="text"
      class="mt-10 border-2 rounded mr-2 p-2"
      v-model="newLabel"
      placeholder="Color"
    />

    <input
      type="text"
      class="mt-10 border-2 rounded mr-2 p-2"
      v-model="newItem"
      placeholder="Percentage"
    />
    <button
      @click="updateChart()"
      class="text-white bg-blue-500 font-bold py-2 px-4 rounded border-none"
    >
      Add
    </button>
  </div>
</template>

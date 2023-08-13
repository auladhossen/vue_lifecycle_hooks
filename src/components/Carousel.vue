<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from "vue";

const items = ref([
  "https://images.unsplash.com/photo-1691030133693-84d7bbec65a2?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80",
  "https://images.unsplash.com/photo-1691074624553-9a215cc2b06e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=968&q=80",
  "https://images.unsplash.com/photo-1691172346369-a76c308ff326?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=929&q=80",
  "https://images.unsplash.com/photo-1691112145993-9e072199c191?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=900&q=80",
]);
let carousel = null;

const newItem = ref(
  "https://images.unsplash.com/photo-1549300461-11c5b94e8855?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80"
);

function addNewItem() {
  items.value.push(newItem.value);
  carousel.destroy();
  nextTick(function () {
    carousel = new Flickity("#carousel", {});
  });
}

onMounted(() => {
  carousel = new Flickity("#carousel", {});
});

onBeforeUnmount(() => {
  carousel.destroy();
});
</script>

<template>
  <div class="my-3">
    <h2 class="my-3 font-bold text-2xl">Carousel</h2>
    <input
      type="text"
      class="border-2 rounded my-3 mx-2 p-2"
      v-model="newItem"
    />
    <button
      @click="addNewItem"
      class="text-white bg-blue-500 font-bold py-2 px-4 rounded border-none"
    >
      Add New Item
    </button>
  </div>
  <div class="items" id="carousel">
    <div
      class="item"
      :style="`background-image:url(${item})`"
      v-for="(item, index) in items"
      :key="index"
    ></div>
  </div>
</template>

<style scoped>
.items {
  width: 500px;
}
.item {
  width: 100%;
  height: 300px;
  background-repeat: no-repeat;
}
</style>

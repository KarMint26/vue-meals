<template>
  <div class="p-8 pb-0 text-rose-500">
    <h1 class="lg:text-3xl sm:text-2xl text-xl font-bold">Random Meals</h1>
  </div>
  <span
    v-if="loading == true"
    class="translate-y-3 loading loading-dots loading-sm sm:loading-md lg:loading-lg block mx-auto text-rose-500"
  ></span>
  <Meals :meals="meals" />
</template>

<script setup>
import { onMounted, ref } from "vue";
import axiosClient from "../axiosClient.js";
import Meals from "../components/Meals.vue";

const meals = ref([]);
const loading = ref(true);

onMounted(async () => {
  setTimeout(() => {
    for (let i = 0; i < 12; i++) {
      axiosClient.get("random.php").then(({ data }) => {
        meals.value.push(data.meals[0]);
      });
    }
    loading.value = false;
  }, 1000);
});
</script>

<style scoped></style>

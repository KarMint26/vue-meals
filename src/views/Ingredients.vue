<template>
  <div class="p-8">
    <h1
      class="text-2xl sm:text-3xl lg:text-4xl font-bold mb-4 text-rose-500"
    >
      Ingredients
    </h1>

    <div class="pt-1 sm:pt-3 pb-5 relative">
      <box-icon
        name="search"
        class="absolute top-[1rem] sm:top-[1.5rem] left-[1rem] z-30"
        color="#989898"
      ></box-icon>
      <input
        type="text"
        v-model="keyword"
        class="input input-bordered w-full relative pl-12"
        placeholder="Search for Ingredients"
      />
    </div>

    <span
      v-if="loading == true"
      class="loading loading-dots loading-sm sm:loading-md lg:loading-lg block mx-auto text-rose-500"
    ></span>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3">
      <router-link
        :to="{
          name: 'byIngredient',
          params: { ingredient: ingredient.strIngredient.toLowerCase() },
        }"
        v-for="ingredient of computedIngredients"
        class="inline-block sm:text-base text-sm bg-white shadow-md rounded-lg p-3 mb-3 hover:scale-[1.03] transition duration-300 ease"
      >
        <img
          :src="`https://www.themealdb.com/images/ingredients/${ingredient.strIngredient}-small.png`"
          class="lg:w-36 sm:w-32 w-28 float-left"
        />
        <h3 class="text-2xl font-bold p-1 text-center leading-1">
          {{ ingredient.strIngredient }}
        </h3>
      </router-link>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import axiosClient from "../axiosClient";

const ingredients = ref([]);
const loading = ref(true);
const keyword = ref("");
const computedIngredients = computed(() => {
  if (!computedIngredients) return ingredients;
  return ingredients.value.filter((i) =>
    i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  );
});

onMounted(() => {
  setTimeout(() => {
    axiosClient.get("list.php?i=list").then(({ data }) => {
      ingredients.value = data.meals;
      loading.value = false;
    });
  }, 1000);
});
</script>

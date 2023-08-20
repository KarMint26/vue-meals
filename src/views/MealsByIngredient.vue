<template>
  <h1 class="text-xl sm:text-2xl lg:text-3xl text-rose-500 font-bold p-8 pb-0">
    Meals for
    {{
      route.params.ingredient[0].toUpperCase() +
      route.params.ingredient
        .slice(1, route.params.ingredient.length)
        .toLowerCase()
    }}
  </h1>
  <span
    v-if="loading == true"
    class="translate-y-5 loading loading-dots loading-sm sm:loading-md lg:loading-lg block mx-auto text-rose-500"
  ></span>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import Meals from "../components/Meals.vue";

const meals = computed(() => store.state.mealsByIngredient);
const route = useRoute();
const loading = ref(true);

onMounted(() => {
  setTimeout(() => {
    store.dispatch("searchMealsByIngredient", route.params.ingredient);
    loading.value = false;
  }, 1000);
});
</script>

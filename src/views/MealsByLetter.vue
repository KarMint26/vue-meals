<template>
  <h1 class="text-xl sm:text-2xl lg:text-3xl text-rose-500 font-bold p-8 pb-0">
    Meals By Letter
  </h1>
  <div class="flex flex-col p-8 pt-4 pb-0 justify-center items-center">
    <div
      class="flex justify-center items-center gap-[0.2rem] sm:gap-2 lg:gap-4 mt-2 sm:text-xl text-sm"
    >
      <router-link
        :to="{ name: 'byLetter', params: { letter } }"
        v-for="letter of letters"
        :key="letter"
        class="hover:scale-150 transition hover:text-rose-500"
      >
        {{ letter }}
      </router-link>
    </div>
  </div>
  <span
    v-if="loading == true && route.params.letter !== ''"
    class="lg:mt-3 sm:mt-2 mt-1 loading loading-dots loading-sm sm:loading-md lg:loading-lg block mx-auto text-rose-500"
  ></span>
  <Meals :meals="meals" />
</template>

<script setup>
import { useRoute } from "vue-router";
import store from "../store";
import { computed, onMounted, watch, ref } from "vue";
import Meals from "../components/Meals.vue";

const route = useRoute();
const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = computed(() => store.state.mealsByLetter);
const loading = ref(true);

watch(route, () => {
  loading.value = true;
  setTimeout(() => {
    store.dispatch("searchMealsByLetter", route.params.letter);
    loading.value = false;
  }, 1000);
});

onMounted(() => {
  setTimeout(() => {
    store.dispatch("searchMealsByLetter", route.params.letter);
    loading.value = false;
  }, 1000);
});
</script>

<template>
  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5 p-8">
    <MealItem v-for="meal of meals" :key="meal.idMeals" :meal="meal" class="hover:scale-[1.03] transition duration-300" />
  </div>
  <div
    v-if="!meals.length"
    class="flex justify-center items-center sm:text-base text-sm text-slate-500 sm:-translate-y-0 -translate-y-8"
  >
    Please Input The Keyword
  </div>
</template>

<script setup>
import MealItem from "./MealItem.vue";

const { meals } = defineProps({
  meals: {
    type: Array,
    required: true,
  },
});
</script>

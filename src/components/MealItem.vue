<template>
  <div class="bg-white shadow-md rounded-xl">
    <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
      <img
        :src="meal.strMealThumb"
        :alt="meal.strMeal"
        class="rounded-t-xl w-full h-48 object-cover"
      />
    </router-link>
    <div class="py-3 px-5 flex flex-col gap-4">
      <h3 class="font-semibold text-slate-800 text-xl">{{ meal.strMeal }}</h3>
      <p v-if="meal.strInstructions != undefined" class="text-slate-500 text-xs sm:text-sm">
        {{ meal.strInstructions.slice(0, 180) }}...
        <router-link
          :to="{ name: 'mealDetails', params: { id: meal.idMeal } }"
          class="text-blue-500"
          >read more</router-link
        >
      </p>
      <div class="flex gap-3">
        <YoutubeButton :href="meal.strYoutube">YouTube</YoutubeButton>
      </div>
    </div>
  </div>
</template>

<script setup>
import YoutubeButton from "../components/YoutubeButton.vue";
const { meal } = defineProps({
  meal: {
    required: true,
    type: Object
  },
});
</script>

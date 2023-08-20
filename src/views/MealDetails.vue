<template>
  <div
    class="w-[300px] sm:w-[600px] lg:w-[800px] mx-auto translate-y-3 lg:translate-y-8"
  >
    <span
      v-if="loading == true"
      class="translate-y-5 loading loading-dots loading-sm sm:loading-md lg:loading-lg block mx-auto text-rose-500"
    ></span>
    <h1 class="lg:text-4xl md:text-3xl text-xl font-bold mb-5">
      {{ meal.strMeal }}
    </h1>
    <img
      :src="meal.strMealThumb"
      :alt="meal.strMeal"
      class="rounded-lg shadow-md"
    />
    <div
      v-if="loading == false"
      class="grid grid-cols-1 text-sm sm:text-lg py-2"
    >
      <div>
        <strong class="font-bold">Category: </strong>{{ meal.strCategory }}
      </div>
      <div><strong class="font-bold">Area: </strong>{{ meal.strArea }}</div>
      <div><strong class="font-bold">Tags: </strong>{{ meal.strTags }}</div>
    </div>
    <div
      v-if="loading == false"
      class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-3 lg:mt-4"
    >
      <div>
        <h2 class="lg:text-2xl sm:text-xl text-lg font-semibold mb-2 lg:mb-3">
          Ingredients
        </h2>
        <ul>
          <template v-for="(i, ind) of new Array(20)">
            <li
              class="text-sm sm:text-base"
              v-if="meal[`strIngredient${ind + 1}`]"
            >
              {{ ind + 1 }}. {{ meal[`strIngredient${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <div class="mt-3 sm:mt-0">
        <h2 class="lg:text-2xl sm:text-xl text-lg font-semibold mb-2 lg:mb-3">
          Measures
        </h2>
        <ul>
          <template v-for="(i, ind) of new Array(20)">
            <li
              class="text-sm sm:text-base"
              v-if="meal[`strMeasure${ind + 1}`]"
            >
              {{ ind + 1 }}. {{ meal[`strMeasure${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
    </div>
    <div v-if="loading == false" class="my-5 sm:my-3">
      <h2
        class="mt-3 lg:mt-6 lg:text-2xl sm:text-xl text-lg font-semibold mb-2 lg:mb-3"
      >
        Instructions
      </h2>
      <p class="sm:text-base text-sm">{{ meal.strInstructions }}</p>
    </div>
    <div
      v-if="loading == false"
      class="w-fit mt-3 lg:mt-6 flex justify-center items-center gap-2 sm:gap-3"
    >
      <YoutubeButton :href="meal.strYoutube">YouTube</YoutubeButton>
      <a
        :href="meal.strSource"
        target="_blank"
        class="sm:px-4 sm:py-3 px-2 py-2 text-xs sm:text-sm bg-orange-500 rounded-lg text-white flex justify-center items-center gap-1"
        ><box-icon name="window-alt" type="solid" color="#ffffff"></box-icon>
        View Original Source ></a
      >
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import YoutubeButton from "../components/YoutubeButton.vue";

const route = useRoute();
const meal = ref([]);
const loading = ref(true);

onMounted(() => {
  setTimeout(() => {
    axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
      meal.value = data.meals[0] || {};
    });
    loading.value = false;
  }, 1000);
});
</script>

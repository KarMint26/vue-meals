<template>
  <h1 class="text-xl sm:text-2xl lg:text-3xl text-rose-500 font-bold p-8 pb-0">Meals By Name</h1>
  <div class="p-8 pt-5 pb-0 relative">
    <box-icon
      name="search"
      class="absolute top-[2rem] left-[3rem] z-30"
      color="#989898"
    ></box-icon>
    <input
      type="text"
      v-model="keyword"
      class="input input-bordered w-full relative pl-12"
      placeholder="Search for Meals"
      @change="searchMeals"
    />
  </div>

  <span
    v-if="loading == true"
    class="lg:mt-3 mt-2 loading loading-dots loading-sm sm:loading-md lg:loading-lg block mx-auto text-rose-500"
  ></span>
  <Meals :meals="meals" />
</template>

<script setup>
import { onMounted, ref } from "vue";
import store from "../store";
import { computed } from "vue";
import { useRoute } from "vue-router";
import Meals from "../components/Meals.vue";

const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);
const loading = ref(false);

function searchMeals() {
  let modifyKeyword =
    keyword.value[0].toUpperCase() +
    keyword.value.slice(1, keyword.value.length).toLowerCase();
  if(modifyKeyword) {
    loading.value = true;
    setTimeout(() => {
      store.dispatch("searchMeals", modifyKeyword);
      loading.value = false;
    }, 1000);
  } else {
    store.commit("setSearchedMeals", []);
  }
}

onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>

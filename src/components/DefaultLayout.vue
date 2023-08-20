<template>
  <div class="bg-gray-100 h-full">
    <Navbar />
    <main class="mt-16">
      <router-view></router-view>
    </main>
  </div>
</template>

<script setup>
import Navbar from './Navbar.vue';
</script>

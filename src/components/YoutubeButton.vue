<template>
  <a
    :href="href"
    target="_blank"
    class="sm:px-4 sm:py-3 px-3 py-2 text-sm bg-rose-500 rounded-lg text-white flex justify-center items-center gap-1"
    ><box-icon name="youtube" type="logo" color="#ffffff"></box-icon> <slot></slot></a
  >
</template>

<script setup>
const props = defineProps({
    href: String
})
</script>
<template>
  <div class="bg-black min-h-screen text-white flex">
    <Sidebar />
    <div class="flex-1 ml-20 lg:ml-64">
      <NuxtPage />
    </div>
  </div>
</template>

<script setup>
import Sidebar from "~/components/Sidebar.vue";
</script>

<style scoped>
/* No changes needed here as Tailwind handles responsiveness */
</style>
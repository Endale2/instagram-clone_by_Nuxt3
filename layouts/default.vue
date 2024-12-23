// File: layouts/default.vue
<template>
  <div class="bg-black min-h-screen text-white flex">
    <Sidebar />
    <div class="flex-1">
      
      <NuxtPage />
    </div>
  </div>
</template>

<script setup>

import Sidebar from "~/components/Sidebar.vue";
</script>

<style scoped>
@import 'tailwindcss/tailwind.css';
</style>

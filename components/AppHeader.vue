<template>
  <header
    class="fixed top-0 left-0 right-0 bg-black border-b border-gray-800 h-14 flex items-center justify-between px-4 z-30 md:hidden"
  >
    <!-- Instagram logo -->
    <InstagramLogo />

    <!-- Right Icons -->
    <div class="flex items-center space-x-5">
      <button class="text-white hover:text-gray-300 transition instagram-hover">
        <Plus class="h-6 w-6" />
      </button>
      <button class="text-white hover:text-gray-300 transition relative instagram-hover">
        <Heart class="h-6 w-6" />
        <!-- Optional red dot -->
        <!-- <span class="absolute -top-1 -right-1 h-2 w-2 bg-red-500 rounded-full"></span> -->
      </button>
      
    </div>
  </header>
</template>

<script setup>
import { Plus, Heart } from 'lucide-vue-next'
</script>

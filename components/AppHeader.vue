<template>
  <header
    class="fixed top-0 left-0 right-0 bg-black border-b border-gray-800 h-14 flex items-center justify-between px-4 z-30 md:hidden"
  >
    <!-- Instagram logo -->
    <img
      src="/images/instagram-text.png"
      alt="Instagram"
      class="h-6 w-auto cursor-pointer instagram-hover"
    />

    <!-- Right Icons -->
    <div class="flex items-center space-x-5">
      <button class="text-white hover:text-gray-300 transition instagram-hover">
        <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
          <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/>
        </svg>
      </button>
      <button class="text-white hover:text-gray-300 transition relative instagram-hover">
        <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
          <path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"/>
        </svg>
        <!-- Optional red dot -->
        <!-- <span class="absolute -top-1 -right-1 h-2 w-2 bg-red-500 rounded-full"></span> -->
      </button>
      
    </div>
  </header>
</template>

<script setup>
// No imports needed - using inline SVG icons
</script>

<template>
  <div class="relative flex items-center p-4 border-b border-gray-800 bg-black justify-center">
    <!-- Left Scroll Button -->
    <button
      @click="scrollLeft"
      class="absolute left-4 z-10 h-10 w-10 bg-black/60 rounded-full flex items-center justify-center text-white hover:bg-black/80 focus:outline-none"
    >
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-6 h-6">
        <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
      </svg>
    </button>

    <!-- Stories Container -->
    <div
      ref="scrollContainer"
      class="flex overflow-x-auto hide-scrollbar space-x-4 max-w-[600px] mx-auto"
    >
      <div
        v-for="n in 10"
        :key="n"
        class="flex flex-col items-center min-w-[80px] shrink-0"
      >
        <div class="relative">
          <!-- Story Profile Image with Gradient Border -->
          <div class="rounded-full p-[2px] bg-gradient-to-tr from-yellow-400 via-pink-500 to-red-500">
            <img
              src="/images/profile.png"
              alt="Story"
              class="h-16 w-16 rounded-full border border-black"
            />
          </div>
          <!-- New Story Indicator -->
          <span
            v-if="n === 1"
            class="absolute bottom-0 right-0 bg-blue-500 rounded-full border border-black h-5 w-5 flex items-center justify-center text-white text-sm font-bold"
          >
            +
          </span>
        </div>
        <!-- Username -->
        <span class="text-xs text-gray-400 mt-2 truncate w-16 text-center">username</span>
      </div>
    </div>

    <!-- Right Scroll Button -->
    <button
      @click="scrollRight"
      class="absolute right-4 z-10 h-10 w-10 bg-black/60 rounded-full flex items-center justify-center text-white hover:bg-black/80 focus:outline-none"
    >
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-6 h-6">
        <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
      </svg>
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const scrollContainer = ref(null);

function scrollLeft() {
  if (scrollContainer.value) {
    scrollContainer.value.scrollBy({
      left: -200,
      behavior: 'smooth',
    });
  }
}

function scrollRight() {
  if (scrollContainer.value) {
    scrollContainer.value.scrollBy({
      left: 200,
      behavior: 'smooth',
    });
  }
}
</script>

<style scoped>
@import 'tailwindcss/tailwind.css';

.hide-scrollbar::-webkit-scrollbar {
  display: none;
}

.hide-scrollbar {
  scrollbar-width: none;
}
</style>

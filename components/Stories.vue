<template>
  <div class="relative flex items-center p-4 border-b border-gray-800 bg-black justify-center">
    <!-- Left Scroll Button -->
    <button
      v-show="!isAtStart"
      @click="scrollLeft"
      class="absolute left-4 z-10 h-8 w-8 bg-white rounded-full flex items-center justify-center text-black hover:bg-gray-200 focus:outline-none shadow"
    >
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-5 h-5">
        <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
      </svg>
    </button>

    <!-- Stories Container -->
    <div
      ref="scrollContainer"
      class="flex overflow-x-auto hide-scrollbar space-x-4 max-w-[600px] lg:max-w-[900px] mx-auto"
      @scroll="checkScrollPosition"
    >
      <div
        v-for="story in stories"
        :key="story.id"
        class="flex flex-col items-center min-w-[80px] shrink-0"
      >
        <div class="relative">
          <!-- Story Profile Image with Gradient Border -->
          <div class="rounded-full p-[2px] bg-gradient-to-tr from-yellow-400 via-pink-500 to-red-500">
            <img
              :src="story.image"
              :alt="story.username"
              class="h-16 w-16 rounded-full border border-black"
            />
          </div>
         
        </div>
        <!-- Username -->
        <span class="text-xs text-gray-400 mt-2 truncate w-16 text-center">
          {{ story.username }}
        </span>
      </div>
    </div>

    <!-- Right Scroll Button -->
    <button
      v-show="!isAtEnd"
      @click="scrollRight"
      class="absolute right-4 z-10 h-8 w-8 bg-white rounded-full flex items-center justify-center text-black hover:bg-gray-200 focus:outline-none shadow"
    >
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-5 h-5">
        <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
      </svg>
    </button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const scrollContainer = ref(null);
const isAtStart = ref(true);
const isAtEnd = ref(false);

const stories = ref([
  { id: 1, username: 'you', image: '/images/profile.png', isNew: true },
  { id: 2, username: 'john_doe', image: '/images/john_doe.png', isNew: false },
  { id: 3, username: 'jane', image: '/images/jane.png', isNew: false },
  { id: 4, username: 'mike', image: '/images/mike.png', isNew: false },
  { id: 5, username: 'emily', image: '/images/emily.png', isNew: false },
  { id: 6, username: 'david', image: '/images/david.png', isNew: false },
  { id: 7, username: 'sarah', image: '/images/sarah.png', isNew: false },
  { id: 8, username: 'alex', image: '/images/alex.png', isNew: false },
]);

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

function checkScrollPosition() {
  const container = scrollContainer.value;

  if (container) {
    const scrollLeft = container.scrollLeft;
    const maxScrollLeft = container.scrollWidth - container.clientWidth;

    isAtStart.value = scrollLeft === 0;
    isAtEnd.value = scrollLeft >= maxScrollLeft;
  }
}

onMounted(() => {
  checkScrollPosition();
});
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

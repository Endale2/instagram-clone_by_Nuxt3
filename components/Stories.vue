<template>
  <div
    class="relative flex items-center
           border-b border-gray-800 bg-black
           w-full
           px-0
           sm:px-4
           py-3
           fade-in"
  >
   <button
      v-show="!isAtStart"
      @click="scrollLeft"
      class="absolute left-1 sm:left-2 z-10 h-8 w-8
             bg-white rounded-full flex items-center justify-center
             text-black hover:bg-gray-200 focus:outline-none shadow-md
             transition-all duration-200 instagram-hover"
    >
      <ChevronLeft class="w-5 h-5" />
    </button>

 <div
  ref="scrollContainer"
  class="flex w-full space-x-3 sm:space-x-4 overflow-x-auto stories-scrollbar touch-auto snap-x snap-mandatory"
  @scroll="checkScrollPosition"
>


      <div class="flex flex-col items-center min-w-[80px] sm:min-w-[90px] shrink-0 relative">
        <div class="relative">
          <img
            :src="stories[0].image"
            :alt="stories[0].username"
            class="h-16 w-16 sm:h-20 sm:w-20 rounded-full border-2 border-gray-700 object-cover instagram-hover"
          />
          <div
            class="absolute bottom-0 right-0 bg-blue-500 rounded-full h-6 w-6 flex items-center justify-center border-2 border-black"
          >
            <Plus class="w-3 h-3 text-white" />
          </div>
        </div>
        <span class="text-xs text-white font-semibold mt-1 truncate w-16 sm:w-20 text-center">
          {{ stories[0].username }}
        </span>
      </div>

      <div
        v-for="story in stories.slice(1)"
        :key="story.id"
        class="flex flex-col items-center min-w-[80px] sm:min-w-[90px] shrink-0"
      >
        <div class="relative">
          <div
            :class="[
              'rounded-full p-[2px]',
              story.isNew ? 'bg-gradient-to-tr from-yellow-400 via-pink-500 to-red-500' : 'border-2 border-gray-700'
            ]"
          >
            <img
              :src="story.image"
              :alt="story.username"
              class="h-16 w-16 sm:h-20 sm:w-20 rounded-full border-2 border-black object-cover instagram-hover"
            />
          </div>
        </div>
        <span class="text-xs text-gray-400 mt-1 truncate w-16 sm:w-20 text-center">
          {{ story.username }}
        </span>
      </div>
    </div>

    <button
      v-show="!isAtEnd"
      @click="scrollRight"
      class="absolute right-1 sm:right-2 z-10 h-8 w-8
             bg-white rounded-full flex items-center justify-center
             text-black hover:bg-gray-200 focus:outline-none shadow-md
             transition-all duration-200 instagram-hover"
    >
      <ChevronRight class="w-5 h-5" />
    </button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { ChevronLeft, ChevronRight, Plus } from 'lucide-vue-next'

const stories = ref([
  { id: 1, username: 'you', image: '/images/profile.png', isNew: true },
  { id: 2, username: 'john_doe', image: '/images/john_doe.png', isNew: false },
  { id: 3, username: 'jane', image: '/images/jane.png', isNew: true },
  { id: 4, username: 'mike', image: '/images/mike.png', isNew: true },
  { id: 5, username: 'emily', image: '/images/emily.png', isNew: false },
  { id: 6, username: 'alex', image: '/images/alex.png', isNew: true },
  { id: 7, username: 'sarah', image: '/images/sarah.png', isNew: false },
  { id: 8, username: 'david', image: '/images/david.png', isNew: true },
  { id: 9, username: 'olivia', image: '/images/olivia.png', isNew: false },
  { id: 10, username: 'chris', image: '/images/chris.png', isNew: true },
]);
const scrollContainer = ref(null)
const isAtStart = ref(true)
const isAtEnd = ref(false)

function scrollLeft() {
  if (scrollContainer.value) {
    scrollContainer.value.scrollBy({
      left: -200, // Adjust scroll amount as needed
      behavior: 'smooth',
    });
  }
}
function scrollRight() {
  if (scrollContainer.value) {
    scrollContainer.value.scrollBy({
      left: 200, // Adjust scroll amount as needed
      behavior: 'smooth',
    });
  }
}
function checkScrollPosition() {
  const container = scrollContainer.value;
  if (container) {
    const scrollLeft = container.scrollLeft;
    const maxScrollLeft = container.scrollWidth - container.clientWidth;
    // Added a small tolerance (e.g., 5px) for browser inconsistencies
    isAtStart.value = scrollLeft <= 5;
    isAtEnd.value = scrollLeft + container.clientWidth >= container.scrollWidth - 5;
  }
}

onMounted(() => {
  checkScrollPosition()
  const resizeObserver = new ResizeObserver(() => checkScrollPosition())
  if (scrollContainer.value) resizeObserver.observe(scrollContainer.value)
})
</script>

<style scoped>
.stories-scrollbar {
  -ms-overflow-style: none;       /* IE/Edge */
  scrollbar-width: none;          /* Firefox */
  -webkit-overflow-scrolling: touch; /* iOS smooth scrolling */
}

.stories-scrollbar::-webkit-scrollbar {
  display: none;                  /* Chrome, Safari */
}

.hide-scrollbar {
  -ms-overflow-style: none;       /* IE/Edge */
  scrollbar-width: none;          /* Firefox */
  -webkit-overflow-scrolling: touch; /* iOS smooth scrolling */
}

.hide-scrollbar::-webkit-scrollbar {
  display: none;                  /* Chrome, Safari */
}
</style>
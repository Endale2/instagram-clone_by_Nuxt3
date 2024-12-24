<template>
  <aside
    :class="[
      'bg-black text-gray-300 h-screen fixed top-0 left-0 flex flex-col items-start p-4 transition-all duration-300',
      isSearchActive ? 'w-96' : 'w-20'
    ]"
  >
    <!-- Instagram Logo -->
    <div
      class="text-white text-2xl font-bold mb-6"
      v-if="!isSearchActive"
    >
      <Icon icon="mdi:instagram" class="h-8 w-8" />
    </div>

    <div
      v-if="isSearchActive"
      class="text-white text-xl font-bold mb-6"
    >
      Search
    </div>

    <!-- Menu Items -->
    <nav class="flex flex-col space-y-6 w-full">
      <a href="#" class="flex items-center space-x-4 text-white font-medium hover:text-gray-400">
        <Icon icon="mdi:home-outline" class="h-6 w-6" />
        <span v-if="isSearchActive" class="label">Home</span>
      </a>
      <a
        @click="toggleSearch"
        class="flex items-center space-x-4 hover:text-gray-400 cursor-pointer"
      >
        <Icon icon="mdi:magnify" class="h-6 w-6" />
        <span v-if="isSearchActive" class="label">Search</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:compass-outline" class="h-6 w-6" />
        <span v-if="isSearchActive" class="label">Explore</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:play-box-outline" class="h-6 w-6" />
        <span v-if="isSearchActive" class="label">Reels</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:message-outline" class="h-6 w-6" />
        <span v-if="isSearchActive" class="label">Messages</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:bell-outline" class="h-6 w-6" />
        <span v-if="isSearchActive" class="label">Notifications</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:plus-box-outline" class="h-6 w-6" />
        <span v-if="isSearchActive" class="label">Create</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:account-outline" class="h-6 w-6" />
        <span v-if="isSearchActive" class="label">Profile</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:dots-horizontal" class="h-6 w-6" />
        <span v-if="isSearchActive" class="label">More</span>
      </a>
    </nav>

    <!-- Search Bar -->
    <div v-if="isSearchActive" class="search-container w-full mt-6">
      <div class="flex items-center bg-gray-800 rounded-md p-2">
        <Icon icon="mdi:magnify" class="h-5 w-5 text-gray-400" />
        <input
          type="text"
          class="bg-transparent w-full ml-2 text-white focus:outline-none"
          placeholder="Search"
        />
        <button
          class="text-gray-400 hover:text-white"
          @click="toggleSearch"
        >
          <Icon icon="mdi:close" class="h-5 w-5" />
        </button>
      </div>
      <div class="mt-4">
        <h3 class="text-white text-sm font-semibold">Recent</h3>
        <p class="text-gray-400 text-sm mt-2">No recent searches.</p>
      </div>
    </div>
  </aside>
</template>

<script setup>
import { ref } from "vue";
import { Icon } from "@iconify/vue";

const isSearchActive = ref(false);

const toggleSearch = () => {
  isSearchActive.value = !isSearchActive.value;
};
</script>

<style scoped>
@import "tailwindcss/tailwind.css";

/* Sidebar styles */
.search-container input::placeholder {
  color: #9ca3af;
}

/* Smooth transitions */
.label {
  transition: opacity 0.3s ease-in-out;
}
</style>

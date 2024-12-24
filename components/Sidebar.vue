<template>
  <aside class="bg-black text-gray-300 w-64 h-screen fixed top-0 left-0 flex flex-col items-start p-4 space-y-8">
    <!-- Instagram Logo -->
    <div class="text-white text-2xl font-bold mb-4">
      Instagram
    </div>

    <!-- Menu Items -->
    <nav class="flex flex-col space-y-6 w-full">
      <a href="#" class="flex items-center space-x-4 text-white font-medium hover:text-gray-400">
        <Icon icon="mdi:home-outline" class="h-6 w-6" />
        <span class="label">Home</span>
      </a>
      <a @click="toggleSearch" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:magnify" class="h-6 w-6" />
        <span v-if="!isSearchActive" class="label">Search</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:compass-outline" class="h-6 w-6" />
        <span class="label">Explore</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:play-box-outline" class="h-6 w-6" />
        <span class="label">Reels</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:message-outline" class="h-6 w-6" />
        <span class="label">Messages</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:bell-outline" class="h-6 w-6" />
        <span class="label">Notifications</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:plus-box-outline" class="h-6 w-6" />
        <span class="label">Create</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:account-outline" class="h-6 w-6" />
        <span class="label">Profile</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <Icon icon="mdi:dots-horizontal" class="h-6 w-6" />
        <span class="label">More</span>
      </a>
    </nav>

    <!-- Search Bar -->
    <div v-if="isSearchActive" class="search-bar w-full mt-6">
      <input
        type="text"
        class="w-full p-2 rounded bg-gray-800 text-white focus:outline-none"
        placeholder="Search..."
      />
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

/* Animation for the search toggle */
.search-bar {
  transition: all 0.3s ease-in-out;
}

.label {
  transition: opacity 0.3s ease-in-out;
}

nav a:hover .label {
  opacity: 0.8;
}
</style>

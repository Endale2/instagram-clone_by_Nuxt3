<template>
  <footer
    class="fixed bottom-0 left-0 right-0 bg-black border-t border-gray-800 h-14 sm:h-16 flex items-center justify-between px-6 sm:px-10 z-30 md:hidden"
  >
    <!-- Home -->
    <button @click="setActive('Home')" class="text-white instagram-hover">
      <svg
        v-if="activeTab === 'Home'"
        class="h-6 w-6"
        fill="currentColor"
        viewBox="0 0 24 24"
      >
        <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/>
      </svg>
      <svg
        v-else
        class="h-6 w-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        stroke-width="2"
      >
        <path stroke-linecap="round" stroke-linejoin="round" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"/>
      </svg>
    </button>

    <!-- Search -->
    <button @click="setActive('Search')" class="text-white instagram-hover">
      <svg
        v-if="activeTab === 'Search'"
        class="h-6 w-6"
        fill="currentColor"
        viewBox="0 0 24 24"
      >
        <path d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
      </svg>
      <svg
        v-else
        class="h-6 w-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        stroke-width="2"
      >
        <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/>
      </svg>
    </button>

    <!-- Create (Plus) -->
    <button @click="setActive('Create')" class="text-white bg-white rounded-full p-1 instagram-hover">
      <svg class="h-5 w-5 text-black" fill="currentColor" viewBox="0 0 24 24">
        <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/>
      </svg>
    </button>

    <!-- Reels -->
    <button @click="setActive('Reels')" class="text-white instagram-hover">
      <svg
        v-if="activeTab === 'Reels'"
        class="h-6 w-6"
        fill="currentColor"
        viewBox="0 0 24 24"
      >
        <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
      </svg>
      <svg
        v-else
        class="h-6 w-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        stroke-width="2"
      >
        <path stroke-linecap="round" stroke-linejoin="round" d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
      </svg>
    </button>

    <!-- Profile (Avatar instead of icon) -->
    <button @click="setActive('Profile')" class="relative instagram-hover">
      <img
        :src="currentUser.avatar"
        alt="Profile"
        class="h-6 w-6 rounded-full border-2"
        :class="activeTab === 'Profile' ? 'border-white' : 'border-gray-500'"
      />
    </button>
  </footer>
</template>

<script setup>
import { ref } from 'vue'

const activeTab = ref('Home')
const setActive = (tab) => (activeTab.value = tab)

const currentUser = {
  username: 'you',
  avatar: '/images/profile.png', // replace with actual image path
}
</script>

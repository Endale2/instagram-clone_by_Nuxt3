<template>
  <footer
    class="fixed bottom-0 left-0 right-0 bg-black border-t border-gray-800 h-14 sm:h-16 flex items-center justify-between px-6 sm:px-10 z-30 md:hidden"
  >
    <!-- Home -->
    <button @click="setActive('Home')" class="text-white">
      <component
        :is="activeTab === 'Home' ? HomeSolid : HomeOutline"
        class="h-6 w-6"
      />
    </button>

    <!-- Search -->
    <button @click="setActive('Search')" class="text-white">
      <component
        :is="activeTab === 'Search' ? SearchSolid : SearchOutline"
        class="h-6 w-6"
      />
    </button>

    <!-- Create (Plus) -->
    <button @click="setActive('Create')" class="text-white bg-white rounded-full p-1">
      <PlusIcon class="h-5 w-5 text-black" />
    </button>

    <!-- Reels -->
    <button @click="setActive('Reels')" class="text-white">
      <component
        :is="activeTab === 'Reels' ? ReelsSolid : ReelsOutline"
        class="h-6 w-6"
      />
    </button>

    <!-- Profile (Avatar instead of icon) -->
    <button @click="setActive('Profile')" class="relative">
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
import {
  HomeIcon as HomeOutline,
  MagnifyingGlassIcon as SearchOutline,
  PlayCircleIcon as ReelsOutline,
} from '@heroicons/vue/24/outline'

import {
  HomeIcon as HomeSolid,
  MagnifyingGlassIcon as SearchSolid,
  PlayCircleIcon as ReelsSolid,
} from '@heroicons/vue/24/solid'

import { PlusIcon } from '@heroicons/vue/24/outline'

const activeTab = ref('Home')
const setActive = (tab) => (activeTab.value = tab)

const currentUser = {
  username: 'you',
  avatar: '/images/profile.png', // replace with actual image path
}
</script>

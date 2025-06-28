<template>
  <footer
    class="fixed bottom-0 left-0 right-0 bg-black border-t border-gray-800 h-14 sm:h-16 flex items-center justify-between px-6 sm:px-10 z-30 md:hidden"
  >
    <!-- Home -->
    <button @click="setActive('Home')" class="text-white instagram-hover">
      <Home
        v-if="activeTab === 'Home'"
        class="h-6 w-6"
        fill="currentColor"
      />
      <Home
        v-else
        class="h-6 w-6"
      />
    </button>

    <!-- Search -->
    <button @click="setActive('Search')" class="text-white instagram-hover">
      <Search
        v-if="activeTab === 'Search'"
        class="h-6 w-6"
        fill="currentColor"
      />
      <Search
        v-else
        class="h-6 w-6"
      />
    </button>

    <!-- Create (Plus) -->
    <button @click="setActive('Create')" class="text-white bg-white rounded-full p-1 instagram-hover">
      <Plus class="h-5 w-5 text-black" />
    </button>

    <!-- Reels -->
    <button @click="setActive('Reels')" class="text-white instagram-hover">
      <Play
        v-if="activeTab === 'Reels'"
        class="h-6 w-6"
        fill="currentColor"
      />
      <Play
        v-else
        class="h-6 w-6"
      />
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
import { Home, Search, Plus, Play } from 'lucide-vue-next'

const activeTab = ref('Home')
const setActive = (tab) => (activeTab.value = tab)

const currentUser = {
  username: 'you',
  avatar: '/images/profile.png', // replace with actual image path
}
</script>

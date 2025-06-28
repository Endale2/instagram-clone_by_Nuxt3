<template>
  <aside class="bg-black text-gray-300 w-18 sm:w-20 md:w-56 lg:w-60 h-screen fixed top-0 left-0 flex flex-col items-center lg:items-start p-2 sm:p-4 lg:p-6 space-y-4 border-r border-gray-800 z-20">
    <div class="mb-6 mt-2 hidden lg:block">
      <InstagramLogo />
    </div>
    <div class="mb-6 mt-2 lg:hidden">
      <div class="h-8 w-8 flex items-center justify-center">
        <span class="text-2xl">📷</span>
      </div>
    </div>
    <nav class="flex flex-col space-y-2 w-full">
      <a
        v-for="item in navItems"
        :key="item.name"
        href="#"
        :class="[
          'flex items-center rounded-lg py-2 px-3 group',
          'justify-center lg:justify-start space-x-4',
          'hover:bg-gray-800 transition-colors duration-200 instagram-hover',
          item.name === 'Home' ? 'text-white font-semibold' : 'text-gray-300',
        ]"
      >
        <component :is="item.name === 'Home' ? item.activeIcon : item.icon" class="h-6 w-6" />
        <span :class="['hidden lg:block text-base', item.name === 'Home' ? 'font-bold' : 'font-medium']">
          {{ item.name }}
        </span>
      </a>
    </nav>
    <div class="mt-auto w-full">
      <a href="#" class="flex items-center justify-center lg:justify-start space-x-4 py-2 px-3 rounded-lg hover:bg-gray-800 transition-colors duration-200 text-gray-300 instagram-hover">
        <MoreHorizontal class="h-6 w-6" />
        <span class="hidden lg:block text-base font-medium">More</span>
      </a>
    </div>
  </aside>
</template>

<script setup>
import { ref } from 'vue'
import { 
  Home, 
  Search, 
  Grid3X3, 
  Play, 
  MessageCircle, 
  Heart, 
  Plus, 
  User,
  MoreHorizontal
} from 'lucide-vue-next'

const navItems = ref([
  { 
    name: 'Home', 
    icon: Home, 
    activeIcon: Home
  },
  { 
    name: 'Search', 
    icon: Search, 
    activeIcon: Search
  },
  { 
    name: 'Explore', 
    icon: Grid3X3, 
    activeIcon: Grid3X3
  },
  { 
    name: 'Reels', 
    icon: Play, 
    activeIcon: Play
  },
  { 
    name: 'Messages', 
    icon: MessageCircle, 
    activeIcon: MessageCircle
  },
  { 
    name: 'Notifications', 
    icon: Heart, 
    activeIcon: Heart
  },
  { 
    name: 'Create', 
    icon: Plus, 
    activeIcon: Plus
  },
  { 
    name: 'Profile', 
    icon: User, 
    activeIcon: User
  },
])
</script>

<style scoped>
/* Tailwind handles styling */
</style>
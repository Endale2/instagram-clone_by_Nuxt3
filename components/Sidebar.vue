### Updated Sidebar.vue
<template>
  <aside class="bg-black text-gray-300 w-64 h-screen fixed top-0 left-0 flex flex-col items-start p-4 space-y-8">
    <!-- Instagram Logo -->
    <div class="text-white text-2xl font-bold mb-4">
      Instagram
    </div>

    <!-- Menu Items -->
    <nav class="flex flex-col space-y-6 w-full">
      <a href="#" class="flex items-center space-x-4 text-white font-medium hover:text-gray-400">
        <HomeIcon class="h-6 w-6" />
        <span>Home</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <MagnifyingGlassIcon class="h-6 w-6" />
        <span>Search</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
          <GlobeAltIcon class="h-6 w-6" />
        <span>Explore</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <FilmIcon class="h-6 w-6" />
        <span>Reels</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <EnvelopeIcon class="h-6 w-6" />
        <span>Messages</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <BellIcon class="h-6 w-6" />
        <span>Notifications</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <PlusIcon class="h-6 w-6" />
        <span>Create</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <UserIcon class="h-6 w-6" />
        <span>Profile</span>
      </a>
      <a href="#" class="flex items-center space-x-4 hover:text-gray-400">
        <EllipsisHorizontalIcon class="h-6 w-6" />
        <span>More</span>
      </a>
    </nav>
  </aside>
</template>

<script setup>
import {
  HomeIcon,
  MagnifyingGlassIcon,
  GlobeAltIcon,
  FilmIcon,
  EnvelopeIcon,
  BellIcon,
  PlusIcon,
  UserIcon,
  EllipsisHorizontalIcon,
} from '@heroicons/vue/24/outline';
</script>

<style scoped>
@import 'tailwindcss/tailwind.css';
</style>

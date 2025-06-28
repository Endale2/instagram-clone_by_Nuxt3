<template>
  <aside class="bg-black text-gray-300 w-18 sm:w-20 md:w-56 lg:w-60 h-screen fixed top-0 left-0 flex flex-col items-center lg:items-start p-2 sm:p-4 lg:p-6 space-y-4 border-r border-gray-800 z-20">
    <div class="mb-6 mt-2 hidden lg:block">
      <img src="/images/instagram-text.png" alt="Instagram" class="h-8 w-auto instagram-hover" />
    </div>
    <div class="mb-6 mt-2 lg:hidden">
      <img src="/images/instagram-icon.png" alt="Instagram" class="h-8 w-8 instagram-hover" />
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
        <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
          <path d="M12 8c1.1 0 2-.9 2-2s-.9-2-2-2-2 .9-2 2 .9 2 2 2zm0 2c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2zm0 6c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/>
        </svg>
        <span class="hidden lg:block text-base font-medium">More</span>
      </a>
    </div>
  </aside>
</template>

<script setup>
import { ref } from 'vue'

const navItems = ref([
  { 
    name: 'Home', 
    icon: {
      template: `<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"/>
      </svg>`
    }, 
    activeIcon: {
      template: `<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
        <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/>
      </svg>`
    } 
  },
  { 
    name: 'Search', 
    icon: {
      template: `<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/>
      </svg>`
    }, 
    activeIcon: {
      template: `<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
        <path d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
      </svg>`
    } 
  },
  { 
    name: 'Explore', 
    icon: {
      template: `<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"/>
      </svg>`
    }, 
    activeIcon: {
      template: `<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
        <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
      </svg>`
    } 
  },
  { 
    name: 'Reels', 
    icon: {
      template: `<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
      </svg>`
    }, 
    activeIcon: {
      template: `<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
        <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
      </svg>`
    } 
  },
  { 
    name: 'Messages', 
    icon: {
      template: `<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"/>
      </svg>`
    }, 
    activeIcon: {
      template: `<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
        <path d="M20 2H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h4l4 4 4-4h4c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2z"/>
      </svg>`
    } 
  },
  { 
    name: 'Notifications', 
    icon: {
      template: `<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"/>
      </svg>`
    }, 
    activeIcon: {
      template: `<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
        <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
      </svg>`
    } 
  },
  { 
    name: 'Create', 
    icon: {
      template: `<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"/>
      </svg>`
    }, 
    activeIcon: {
      template: `<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
        <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/>
      </svg>`
    } 
  },
  { 
    name: 'Profile', 
    icon: {
      template: `<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"/>
      </svg>`
    }, 
    activeIcon: {
      template: `<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
        <path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/>
      </svg>`
    } 
  },
])
</script>

<style scoped>
/* Tailwind handles styling */
</style>
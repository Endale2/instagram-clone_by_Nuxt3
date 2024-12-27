<template>
  <aside
    class="bg-black text-gray-300 w-20 lg:w-64 h-screen fixed top-0 left-0 flex flex-col items-center lg:items-start p-4 space-y-8"
  >
    <!-- Instagram Logo -->
    <div class="text-white text-2xl font-bold mb-4 lg:block hidden">
      Instagram Clone
    </div>

    <!-- Menu Items -->
    <nav class="flex flex-col space-y-6 w-full">
      <a
        href="#"
        class="flex items-center justify-center lg:justify-start space-x-4 text-white font-medium hover:text-gray-400 active-nav"
      >
        <Icon icon="mdi:home-outline" class="h-6 w-6" />
        <span class="hidden lg:block">Home</span>
      </a>
      <a
        href="#"
        class="flex items-center justify-center lg:justify-start space-x-4 hover:text-gray-400"
      >
        <Icon icon="mdi:magnify" class="h-6 w-6" />
        <span class="hidden lg:block">Search</span>
      </a>
      <a
        href="#"
        class="flex items-center justify-center lg:justify-start space-x-4 hover:text-gray-400"
      >
        <Icon icon="mdi:compass-outline" class="h-6 w-6" />
        <span class="hidden lg:block">Explore</span>
      </a>
      <a
        href="#"
        class="flex items-center justify-center lg:justify-start space-x-4 hover:text-gray-400"
      >
        <Icon icon="mdi:play-box-outline" class="h-6 w-6" />
        <span class="hidden lg:block">Reels</span>
      </a>
      <a
        href="#"
        class="flex items-center justify-center lg:justify-start space-x-4 hover:text-gray-400"
      >
        <Icon icon="mdi:message-outline" class="h-6 w-6" />
        <span class="hidden lg:block">Messages</span>
      </a>
      <a
        href="#"
        class="flex items-center justify-center lg:justify-start space-x-4 hover:text-gray-400"
      >
        <Icon icon="mdi:bell-outline" class="h-6 w-6" />
        <span class="hidden lg:block">Notifications</span>
      </a>
      <a
        href="#"
        class="flex items-center justify-center lg:justify-start space-x-4 hover:text-gray-400"
      >
        <Icon icon="mdi:plus-box-outline" class="h-6 w-6" />
        <span class="hidden lg:block">Create</span>
      </a>
      <a
        href="#"
        class="flex items-center justify-center lg:justify-start space-x-4 hover:text-gray-400"
      >
        <Icon icon="mdi:account-outline" class="h-6 w-6" />
        <span class="hidden lg:block">Profile</span>
      </a>
      <a
        href="#"
        class="flex items-center justify-center lg:justify-start space-x-4 hover:text-gray-400"
      >
        <Icon icon="mdi:dots-horizontal" class="h-6 w-6" />
        <span class="hidden lg:block">More</span>
      </a>
    </nav>
  </aside>
</template>

<script setup>
import { Icon } from "@iconify/vue";
</script>

<style scoped>
/* Sidebar Transition */
aside {
  transition: width 0.3s ease-in-out;
}

/* Label Transition */
nav a .hidden {
  transition: opacity 0.3s ease-in-out;
}

nav a:hover .hidden {
  opacity: 0.8;
}

/* Active Navigation Styling */
.active-nav {
  color: white; /* Active blue color */
  font-weight: bold;
}
</style>

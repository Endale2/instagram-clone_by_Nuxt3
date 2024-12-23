<template>
  <div class="p-6 pl-8 w-80 bg-black text-white">
    <!-- Profile Section -->
    <div class="flex items-center space-x-4 mb-8">
      <img
        src="/images/profile.png"
        alt="User Profile"
        class="h-14 w-14 rounded-full"
      />
      <div class="flex-1">
        <p class="font-semibold">cdjkr</p>
        <p class="text-gray-500 text-sm">Endale</p>
      </div>
      <button class="text-blue-400 font-medium text-sm">Switch</button>
    </div>

    <!-- Suggestions Header -->
    <h2 class="text-sm text-gray-400 font-medium mb-4">Suggestions for you</h2>

    <!-- Suggestions List -->
    <div
      v-for="n in 5"
      :key="n"
      class="flex justify-between items-center mb-4"
    >
      <div class="flex items-center space-x-3">
        <img
          src="/images/profile.png"
          alt="Suggested User"
          class="h-10 w-10 rounded-full"
        />
        <div>
          <p class="font-semibold text-sm">username</p>
          <p class="text-gray-500 text-xs">Instagram recommended</p>
        </div>
      </div>
      <button class="text-blue-400 font-medium text-sm">Follow</button>
    </div>

    <!-- Footer -->
    <div class="mt-8 text-xs text-gray-500 space-y-1 leading-5">
      <p>About • Help • Press • API • Jobs • Privacy • Terms • Locations</p>
      <p>Language</p>
      <p class="mt-2">© 2024 Instagram from Meta</p>
    </div>
  </div>
</template>

<script setup>
// No additional logic needed for this static component
</script>

<style scoped>
@import 'tailwindcss/tailwind.css';
</style>

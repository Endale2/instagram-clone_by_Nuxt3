<template>
  <div class="p-6 pl-8 w-80 bg-black text-white relative">
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
      v-for="(user, index) in suggestions"
      :key="user.id"
      class="flex justify-between items-center mb-4 relative group"
    >
      <!-- User Info -->
      <div class="flex items-center space-x-3">
        <img
          :src="user.image"
          alt="Suggested User"
          class="h-10 w-10 rounded-full"
        />
        <div>
          <div class="flex items-center space-x-1">
            <p class="font-semibold text-sm">{{ user.username }}</p>
            <svg
              v-if="user.verified"
              xmlns="http://www.w3.org/2000/svg"
              class="h-4 w-4 text-blue-500"
              viewBox="0 0 20 20"
              fill="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-10.293a1 1 0 00-1.414 0L9 11l-1.293-1.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4a1 1 0 000-1.414z"
                clip-rule="evenodd"
              />
            </svg>
          </div>
          <p class="text-gray-500 text-xs">Instagram recommended</p>
        </div>
      </div>
      <button 
        @click="toggleFollow(user)"
        :class="user.following ? 'text-gray-400' : 'text-blue-400'"
        class="font-medium text-sm"
      >
        {{ user.following ? 'Following' : 'Follow' }}
      </button>

      <!-- Hover Profile Card -->
      <div
        class="absolute -left-8 top-12 w-100 bg-black text-white border border-gray-700 rounded-lg p-4 shadow-lg hidden group-hover:flex flex-col space-y-4 z-10"
      >
        <!-- Profile Info -->
        <div class="flex items-center space-x-3">
          <img
            :src="user.image"
            alt="User Profile"
            class="h-14 w-14 rounded-full"
          />
          <div>
            <div class="flex items-center space-x-1">
              <p class="font-semibold text-lg">{{ user.username }}</p>
              <svg
                v-if="user.verified"
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 text-blue-500"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-10.293a1 1 0 00-1.414 0L9 11l-1.293-1.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4a1 1 0 000-1.414z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
            <p class="text-gray-400 text-sm">{{ user.fullName }}</p>
          </div>
        </div>

        <!-- Stats -->
        <div class="flex justify-between text-sm text-gray-400">
          <div class="flex flex-col items-center">
            <p class="font-bold text-white">{{ user.posts }}</p>
            <p>posts</p>
          </div>
          <div class="flex flex-col items-center">
            <p class="font-bold text-white">{{ user.followers }}</p>
            <p>followers</p>
          </div>
          <div class="flex flex-col items-center">
            <p class="font-bold text-white">{{ user.following }}</p>
            <p>following</p>
          </div>
        </div>

        <!-- Recent Posts -->
        <div class="grid grid-cols-3 gap-1">
          <img
            v-for="(img, i) in user.recentPosts"
            :key="i"
            :src="img"
            alt="Recent Post"
            class="h-16 w-full object-cover rounded"
          />
        </div>

        <!-- Follow Button -->
        <button
          @click="toggleFollow(user)"
          class="bg-blue-500 text-white text-sm font-medium py-2 px-4 rounded hover:bg-blue-600"
        >
          + Follow
        </button>
      </div>
    </div>

    <!-- Footer -->
    <div class="mt-8 text-xs text-gray-500 space-y-1 leading-5">
      <p>About • Help • Press • API • Jobs • Privacy • Terms • Locations</p>
      <p>Language</p>
      <p class="mt-2">© 2024 Instagram Clone By Endale</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Sample Suggestions Data
const suggestions = ref([
  {
    id: 1,
    username: 'cristiano',
    fullName: 'Cristiano Ronaldo',
    image: '/images/ronaldo.png',
    posts: 3808,
    followers: '645M',
    following: 589,
    verified: true,
    recentPosts: ['/images/ronaldo1.png', '/images/ronaldo2.png', '/images/ronaldo3.png'],
  },
  {
    id: 2,
    username: 'kevinhart4real',
    fullName: 'Kevin Hart',
    image: '/images/kevinhart.png',
    posts: 9429,
    followers: '178M',
    following: 1144,
    verified: true,
    recentPosts: ['/images/kevin1.png', '/images/kevin2.png', '/images/kevin3.png'],
  },
  {
    id: 3,
    username: 'Janet_23',
    fullName: 'Janet',
    image: '/images/jane.png',
    posts: 20,
    followers: '78.8k',
    following: 4112,
    verified: false,
    recentPosts: ['/images/jane.png', '/images/sarah.png', '/images/emily.png'],
  },
  {
    id: 3,
    username: 'daniel34',
    fullName: 'Daniel',
    image: '/images/mike.png',
    posts: 200,
    followers: '15.8k',
    following: 400,
    verified: false,
    recentPosts: ['/images/david.png', '/images/john_doe.png', '/images/mike.png'],
  },
]);

// Toggle the follow/following state
const toggleFollow = (user) => {
  user.following = !user.following;
};
</script>

<style scoped>
@import 'tailwindcss/tailwind.css';

.group:hover .group-hover\\:flex {
  display: flex !important;
}
</style>

<template>
  <div class="hidden md:block w-80 bg-black text-white pl-8 pr-6 py-6">
    <div class="flex items-center space-x-4 mb-8">
      <img
        src="/images/profile.png"
        alt="User Profile"
        class="h-14 w-14 rounded-full border-2 border-transparent hover:border-gray-700 cursor-pointer"
      />
      <div class="flex-1">
        <p class="font-semibold text-sm">cdjkr</p>
        <p class="text-gray-500 text-sm">Endale</p>
      </div>
      <button class="text-blue-400 font-medium text-xs hover:text-blue-300">Switch</button>
    </div>

    <div class="flex justify-between items-center mb-4">
      <h2 class="text-sm text-gray-400 font-medium">Suggestions for you</h2>
      <button class="text-xs text-white font-semibold hover:text-gray-400">See All</button>
    </div>

    <div
      v-for="(user, index) in suggestions"
      :key="user.id"
      class="flex justify-between items-center mb-4 relative group"
    >
      <div class="flex items-center space-x-3 cursor-pointer">
        <img
          :src="user.image"
          :alt="user.username"
          class="h-9 w-9 rounded-full border border-gray-700 object-cover"
        />
        <div>
          <div class="flex items-center space-x-1">
            <p class="font-semibold text-sm">{{ user.username }}</p>
            <svg
              v-if="user.verified"
              xmlns="http://www.w3.org/2000/svg"
              class="h-3.5 w-3.5 text-blue-500 flex-shrink-0"
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
          <p class="text-gray-500 text-xs truncate w-32">Instagram recommended</p>
        </div>
      </div>
      <button
        @click="toggleFollow(user)"
        :class="user.following ? 'text-gray-400' : 'text-blue-400'"
        class="font-medium text-xs hover:text-blue-300"
      >
        {{ user.following ? 'Following' : 'Follow' }}
      </button>

      <div
        class="absolute -left-10 top-1/2 -translate-y-1/2 w-[340px] bg-black text-white border border-gray-700 rounded-lg p-4 shadow-lg hidden group-hover:flex flex-col space-y-4 z-20"
      >
        <div class="flex items-center space-x-3">
          <img
            :src="user.image"
            alt="User Profile"
            class="h-16 w-16 rounded-full border-2 border-gray-700 object-cover"
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
            <p class="text-gray-400 text-sm truncate">{{ user.fullName }}</p>
          </div>
        </div>

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
            <p class="font-bold text-white">{{ user.following_peoples }}</p>
            <p>following</p>
          </div>
        </div>

        <div class="grid grid-cols-3 gap-1">
          <img
            v-for="(img, i) in user.recentPosts.slice(0, 3)"
            :key="i"
            :src="img"
            alt="Recent Post"
            class="h-20 w-full object-cover rounded"
          />
        </div>

        <button
          @click="toggleFollow(user)"
          :class="user.following ? 'bg-gray-700 hover:bg-gray-600 text-white' : 'bg-blue-500 hover:bg-blue-600 text-white'"
          class="text-sm font-medium py-2 px-4 rounded"
        >
          {{ user.following ? 'Following' : 'Follow' }}
        </button>
      </div>
    </div>

    <div class="mt-8 text-xs text-gray-500 space-y-1 leading-4">
      <p>
        <a href="#" class="hover:underline">About</a> •
        <a href="#" class="hover:underline">Help</a> •
        <a href="#" class="hover:underline">Press</a> •
        <a href="#" class="hover:underline">API</a> •
        <a href="#" class="hover:underline">Jobs</a> •
        <a href="#" class="hover:underline">Privacy</a> •
        <a href="#" class="hover:underline">Terms</a> •
        <a href="#" class="hover:underline">Locations</a>
      </p>
      <p class="mt-2">
        <a href="#" class="hover:underline">Language</a>
      </p>
      <p class="mt-2">© 2024 Instagram Clone By Endale</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const suggestions = ref([
  {
    id: 1,
    username: 'cristiano',
    fullName: 'Cristiano Ronaldo',
    image: '/images/ronaldo.png',
    posts: 3808,
    followers: '645M',
    following: false,
    following_peoples: 446,
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
    following: false,
    following_peoples: 512,
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
    following: false,
    following_peoples: 7065,
    verified: false,
    recentPosts: ['/images/jane.png', '/images/sarah.png', '/images/emily.png'],
  },
  {
    id: 4,
    username: 'daniel34',
    fullName: 'Daniel',
    image: '/images/mike.png',
    posts: 200,
    followers: '15.8k',
    following: false,
    following_peoples: 7065,
    verified: false,
    recentPosts: ['/images/david.png', '/images/john_doe.png', '/images/mike.png'],
  },
]);

const toggleFollow = (user) => {
  user.following = !user.following;
};
</script>

<style scoped>
/* No need for @import 'tailwindcss/tailwind.css'; if configured globally in nuxt.config.js */
/* This specific rule is no longer needed with proper Tailwind setup as group-hover:flex handles it */
/* .group:hover .group-hover\:flex {
  display: flex !important;
} */
</style>
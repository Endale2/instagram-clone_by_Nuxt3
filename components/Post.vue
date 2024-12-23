<template>
  <div
    class="bg-black text-white border border-gray-800 p-4 md:p-6 rounded-lg max-w-full mx-auto lg:max-w-[500px]"
  >
    <!-- Header -->
    <div class="flex items-center space-x-3 mb-3">
      <img
        src="/images/profile.png"
        alt="User Avatar"
        class="h-10 w-10 rounded-full"
      />
      <div>
        <span class="font-medium block leading-tight">username</span>
        <span class="text-sm text-gray-500">1w</span>
      </div>
      <div class="ml-auto">
        <button class="text-gray-400 hover:text-gray-300">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 10h12M6 14h12m-7 4h7m-7-8h7m-7-4h7"
            />
          </svg>
        </button>
      </div>
    </div>

    <!-- Post Image -->
    <div class="relative">
      <img
        src="/images/post-placeholder.png"
        alt="Post"
        class="w-full rounded-lg"
      />
      <div class="absolute bottom-2 right-2 bg-black/60 px-2 py-1 rounded-full text-sm text-white">
        <span>1 / 5</span>
      </div>
    </div>

    <!-- Post Actions -->
    <div class="flex justify-between items-center mt-4">
      <div class="flex space-x-4">
        <HeartIcon class="h-6 w-6 cursor-pointer hover:text-gray-400" />
        <ChatBubbleLeftIcon class="h-6 w-6 cursor-pointer hover:text-gray-400" />
        <PaperAirplaneIcon
          class="h-6 w-6 cursor-pointer hover:text-gray-400 transform rotate-45"
        />
      </div>
      <BookmarkIcon class="h-6 w-6 cursor-pointer hover:text-gray-400" />
    </div>

    <!-- Likes -->
    <p class="mt-4 text-sm font-medium">
      <span>1,009,333</span> likes
    </p>

    <!-- Caption -->
    <p class="mt-2 text-sm leading-6">
      <span class="font-medium truncate">username</span> Season one
      <span class="text-blue-500">@theiconleague</span> in the books! Congrats
      to our first champion <span class="text-blue-500">@onefootball</span> and
      thanks to all teamheads, players... <span class="text-gray-400">more</span>
    </p>

    <!-- Comments Preview -->
    <div class="mt-4 text-sm text-gray-400">
      <p class="hover:text-white cursor-pointer">View all 1,147 comments</p>
      <p>
        <span class="font-medium text-white">user1</span> Amazing work!
      </p>
      <p>
        <span class="font-medium text-white">user2</span> Loved this event!
      </p>
    </div>

    <!-- Add a Comment -->
    <div
      class="mt-6 flex items-center space-x-3 border-t border-gray-700 pt-4"
    >
      <FaceSmileIcon class="h-6 w-6 text-gray-400 shrink-0" />
      <input
        type="text"
        placeholder="Add a comment..."
        class="bg-black text-sm text-gray-400 focus:outline-none flex-1"
      />
      <button class="text-blue-500 font-medium text-sm">Post</button>
    </div>
  </div>
</template>

<script setup>
import {
  HeartIcon,
  ChatBubbleLeftIcon,
  PaperAirplaneIcon,
  BookmarkIcon,
  FaceSmileIcon,
} from "@heroicons/vue/24/outline";
</script>

<style scoped>
@import "tailwindcss/tailwind.css";
</style>

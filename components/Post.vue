<template>
  <div
    v-for="(post, index) in posts"
    :key="index"
    class="bg-black text-white border border-gray-800 p-4 md:p-6 rounded-lg max-w-full mx-auto lg:max-w-[500px]"
  >
    <!-- Header -->
    <div class="flex items-center space-x-3 mb-3">
      <img
        :src="post.user.avatar"
        alt="User Avatar"
        class="h-10 w-10 rounded-full"
      />
      <div class="flex-1">
        <div class="flex items-center space-x-1">
          <span class="font-medium leading-tight">{{ post.user.username }}</span>
          <svg
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
        <span class="text-sm text-gray-500">{{ post.timeAgo }}</span>
      </div>
    </div>

    <!-- Post Content -->
    <div class="relative">
      <div v-if="post.type === 'image'" class="w-full">
        <img :src="post.image" alt="Post" class="w-full rounded-lg" />
      </div>
      <div v-if="post.type === 'carousel'" class="relative">
        <img
          :src="post.images[post.currentImageIndex]"
          alt="Carousel Image"
          class="w-full rounded-lg"
        />
        <button
          class="absolute top-1/2 left-2 transform -translate-y-1/2 bg-black/60 text-white px-2 py-1 rounded-full"
          @click="prevImage(post)"
        >
          &lt;
        </button>
        <button
          class="absolute top-1/2 right-2 transform -translate-y-1/2 bg-black/60 text-white px-2 py-1 rounded-full"
          @click="nextImage(post)"
        >
          &gt;
        </button>
      </div>
    </div>

    <!-- Post Actions -->
    <div class="flex justify-between items-center mt-4">
      <div class="flex space-x-4">
        <button @click="toggleLike(post)">
          <HeartIcon
            :class="['h-6 w-6 cursor-pointer', post.liked ? 'text-red-500' : 'hover:text-gray-400']"
          />
        </button>
        <ChatBubbleLeftIcon class="h-6 w-6 cursor-pointer hover:text-gray-400" />
        <PaperAirplaneIcon
          class="h-6 w-6 cursor-pointer hover:text-gray-400 transform rotate-45"
        />
      </div>
    </div>

    <!-- Likes -->
    <p class="mt-4 text-sm font-medium">
      <span>{{ post.likes }} </span>likes
    </p>

    <!-- Caption -->
    <p class="mt-2 text-sm leading-6">
      <span class="font-medium truncate">{{ post.user.username }}</span>
      {{ post.caption }}
    </p>
  </div>
</template>

<script setup>
import {
  HeartIcon,
  ChatBubbleLeftIcon,
  PaperAirplaneIcon,
} from "@heroicons/vue/24/outline";
import { reactive } from "vue";

// Hardcoded post data
const posts = reactive([
  {
    user: { username: "john_doe", avatar: "/images/john_doe.png" },
    timeAgo: "2h",
    type: "carousel",
    images: ["/images/post-placeholder.png", "/images/post-placeholder1.png", "/images/post-placeholder2.png"],
    currentImageIndex: 0,
    likes: 120,
    liked: false,
    caption: "Exploring the mountains! 🏔️",
  },
  {
    user: { username: "jane_smith", avatar: "/images/jane.png" },
    timeAgo: "1d",
    type: "image",
    image: "/images/post-placeholder1.png",
    likes: 432,
    liked: false,
    caption: "City life never gets old 🌆",
  },
]);

const toggleLike = (post) => {
  post.liked = !post.liked;
  post.likes += post.liked ? 1 : -1;
};

const nextImage = (post) => {
  post.currentImageIndex =
    (post.currentImageIndex + 1) % post.images.length;
};

const prevImage = (post) => {
  post.currentImageIndex =
    (post.currentImageIndex - 1 + post.images.length) % post.images.length;
};
</script>

<style scoped>
@import "tailwindcss/tailwind.css";
</style>

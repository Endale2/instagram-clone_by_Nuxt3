<template>
  <div
    v-for="(post, index) in uniquePosts"
    :key="index"
    class="bg-black text-white border border-gray-800 p-4 md:p-6 rounded-lg max-w-full mx-auto lg:max-w-[500px]"
  >
    <!-- Header with Hover Card -->
    <div class="relative flex items-center justify-between mb-3 group">
      <div class="flex items-center space-x-3">
        <div class="relative">
          <img
            :src="post.user.avatar"
            alt="User Avatar"
            class="h-10 w-10 rounded-full cursor-pointer"
          />
          <div
            class="absolute -left-8 top-12 w-80 bg-black text-white border border-gray-700 rounded-lg p-4 shadow-lg hidden group-hover:flex flex-col space-y-4 z-10"
          >
            <!-- Profile Info -->
            <div class="flex items-center space-x-3">
              <img
                :src="post.user.avatar"
                alt="User Profile"
                class="h-14 w-14 rounded-full"
              />
              <div>
                <div class="flex items-center space-x-1">
                  <p class="font-semibold text-lg">{{ post.user.username }}</p>
                  <CheckCircleIcon
                    v-if="post.user.verified"
                    class="h-5 w-5 text-blue-500"
                  />
                </div>
                <p class="text-gray-400 text-sm">{{ post.user.fullName }}</p>
              </div>
            </div>

            <!-- Stats -->
            <div class="flex justify-between text-sm text-gray-400">
              <div class="flex flex-col items-center">
                <p class="font-bold text-white">{{ post.user.posts }}</p>
                <p>posts</p>
              </div>
              <div class="flex flex-col items-center">
                <p class="font-bold text-white">{{ post.user.followers }}</p>
                <p>followers</p>
              </div>
              <div class="flex flex-col items-center">
                <p class="font-bold text-white">{{ post.user.following }}</p>
                <p>following</p>
              </div>
            </div>

            <!-- Recent Posts -->
            <div class="mt-3">
              <div class="flex space-x-2">
                <img
                  v-for="(recentPost, index) in post.user.recentPosts"
                  :key="index"
                  :src="recentPost"
                  alt="Recent Post"
                  class="h-20 w-20 object-cover rounded-md "
                />
              </div>
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
        <div>
          <span class="font-medium leading-tight cursor-pointer">
            {{ post.user.username }}
          </span>
          <CheckCircleIcon
            v-if="post.user.verified"
            class="h-5 w-5 text-blue-500 inline-block ml-1"
          />
        </div>
      </div>
      <EllipsisHorizontalIcon class="h-6 w-6 text-gray-400 cursor-pointer hover:text-white" />
    </div>

    <!-- Post Content -->
    <div class="relative">
      <div v-if="post.type === 'image'" class="w-full aspect-square">
        <img
          :src="post.image"
          alt="Post"
          class="w-full h-full object-cover rounded-lg"
        />
      </div>
      <div v-if="post.type === 'carousel'" class="relative w-full aspect-square">
        <img
          :src="post.images[post.currentImageIndex]"
          alt="Carousel Image"
          class="w-full h-full object-cover rounded-lg"
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
      <div v-if="post.type === 'video'" class="w-full aspect-square">
        <video
          :src="post.video"
          controls
          class="w-full h-full object-cover rounded-lg"
        ></video>
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
        <Icon icon="emojione:pushpin" class="h-6 w-6 text-gray-400 cursor-pointer hover:text-white" />
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

    <!-- Top Comments -->
    <div class="mt-4 space-y-2">
      <div
        v-for="(comment, index) in post.comments.slice(0, 2)"
        :key="index"
        class="text-sm"
      >
        <span class="font-medium">{{ comment.user }}</span>
        <span>{{ comment.text }}</span>
        <span v-if="comment.emoji" class="ml-2">{{ comment.emoji }}</span>
      </div>
    </div>

    <!-- Comment Input -->
    <div class="mt-4 flex items-center space-x-2">
      <input
        type="text"
        placeholder="Add a comment..."
        class="flex-grow bg-black text-white border-b border-gray-700 px-4 py-2 focus:outline-none"
      />
      <Icon
        icon="emojione:pushpin"
        class="h-6 w-6 text-gray-400 cursor-pointer hover:text-white"
      />
    </div>
  </div>
</template>

<script setup>
import {
  HeartIcon,
  ChatBubbleLeftIcon,
  PaperAirplaneIcon,
  EllipsisHorizontalIcon,
  CheckCircleIcon,
} from "@heroicons/vue/24/outline";
import { Icon } from "@iconify/vue";
import { reactive, computed } from "vue";

const posts = reactive([
 {
    user: {
      username: "john_doe",
      avatar: "/images/john_doe.png",
      fullName: "John Doe",
      verified: true,
      posts: 150,
      followers: 3000,
      following: 500,
      recentPosts: ["/images/post-placeholder.png", "/images/post-placeholder1.png", "/images/post-placeholder2.png"],
    },
    type: "image",
    image: "/images/post-placeholder1.png",
    likes: 120,
    liked: true,
    caption: "A beautiful sunset",
    comments: [
      { user: "emily", text: "Stunning view!", emoji: "😍" },
      { user: "alex", text: "Where is this?", emoji: "📍" },
    ],
  },
  {
    user: {
      username: "emily",
      avatar: "/images/emily.png",
      fullName: "Emily Jones",
      verified: false,
      posts: 90,
      followers: 2000,
      following: 300,
      recentPosts: ["/images/emily.png", "/images/sarah.png"],
    },
    type: "video",
    video: "/videos/sample-video.mp4",
    likes: 85,
    liked: false,
    caption: "A beautiful sunset by the lake 🌅",
    comments: [
      { user: "john_doe", text: "This looks amazing!", emoji: "🔥" },
      { user: "alex", text: "Love it!", emoji: "❤️" },
    ],
  },
  {
    user: {
      username: "alex",
      avatar: "/images/alex.png",
      fullName: "Mark Jones",
      verified: true,
      posts: 200,
      followers: 5000,
      following: 700,
      recentPosts: ["/images/alex.png", "/images/italy.png", "images/paris.png"],
    },
    type: "carousel",
    images: ["/images/paris.png", "/images/italy.png"],
    currentImageIndex: 0,
    likes: 190,
    liked: false,
    caption: "Traveling through Europe 🚆",
    comments: [
      { user: "emily", text: "So jealous!", emoji: "😍" },
      { user: "john_doe", text: "What a trip!", emoji: "✈️" },
    ],
  },
]);

const uniquePosts = computed(() => {
  const seenUsers = new Set();
  return posts.filter((post) => {
    if (seenUsers.has(post.user.username)) {
      return false;
    }
    seenUsers.add(post.user.username);
    return true;
  });
});

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

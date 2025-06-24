<template>
  <div
    v-for="(post, index) in uniquePosts"
    :key="index"
    class="bg-black text-white border border-gray-800 rounded-lg max-w-full sm:max-w-[470px] lg:max-w-[500px] xl:max-w-[600px] mx-auto mb-6"
  >
    <div class="relative flex items-center justify-between p-3 sm:p-4 group">
      <div class="flex items-center space-x-3">
        <div class="relative">
          <img
            :src="post.user.avatar"
            :alt="post.user.username"
            class="h-9 w-9 rounded-full border border-gray-700 cursor-pointer object-cover"
          />
          <div
            class="absolute left-0 top-12 w-[340px] bg-black text-white border border-gray-700 rounded-lg p-4 shadow-lg hidden group-hover:flex flex-col space-y-4 z-20"
          >
            <div class="flex items-center space-x-3">
              <img
                :src="post.user.avatar"
                :alt="post.user.username"
                class="h-16 w-16 rounded-full border-2 border-gray-700 object-cover"
              />
              <div>
                <div class="flex items-center space-x-1">
                  <p class="font-semibold text-lg">{{ post.user.username }}</p>
                  <CheckCircleIcon
                    v-if="post.user.verified"
                    class="h-5 w-5 text-blue-500"
                  />
                </div>
                <p class="text-gray-400 text-sm truncate">{{ post.user.fullName }}</p>
              </div>
            </div>

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

            <div class="grid grid-cols-3 gap-1">
              <img
                v-for="(recentPost, i) in post.user.recentPosts.slice(0, 3)"
                :key="i"
                :src="recentPost"
                alt="Recent Post"
                class="h-20 w-full object-cover rounded"
              />
            </div>

            <button
              @click="toggleUserFollow(post.user)"
              :class="post.user.isFollowing ? 'bg-gray-700 hover:bg-gray-600 text-white' : 'bg-blue-500 hover:bg-blue-600 text-white'"
              class="text-sm font-medium py-2 px-4 rounded"
            >
              {{ post.user.isFollowing ? 'Following' : 'Follow' }}
            </button>
          </div>
        </div>
        <a href="#" class="flex items-center space-x-1">
          <span class="font-semibold text-sm cursor-pointer hover:underline">
            {{ post.user.username }}
          </span>
          <CheckCircleIcon
            v-if="post.user.verified"
            class="h-3.5 w-3.5 text-blue-500 flex-shrink-0"
          />
        </a>
      </div>
      <EllipsisHorizontalIcon class="h-6 w-6 text-gray-400 cursor-pointer hover:text-white" />
    </div>

    <div class="relative w-full aspect-square border-t border-gray-800">
      <div v-if="post.type === 'image'" class="w-full h-full">
        <img :src="post.image" :alt="post.caption" class="w-full h-full object-cover" />
      </div>
      <div v-if="post.type === 'carousel'" class="relative w-full h-full">
        <img
          :src="post.images[post.currentImageIndex]"
          :alt="'Carousel Image ' + (post.currentImageIndex + 1)"
          class="w-full h-full object-cover"
        />
        <button
          v-if="post.currentImageIndex > 0"
          class="absolute top-1/2 left-2 transform -translate-y-1/2 bg-black/60 text-white p-1 rounded-full text-lg opacity-80 hover:opacity-100 transition-opacity"
          @click="prevImage(post)"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd" />
          </svg>
        </button>
        <button
          v-if="post.currentImageIndex < post.images.length - 1"
          class="absolute top-1/2 right-2 transform -translate-y-1/2 bg-black/60 text-white p-1 rounded-full text-lg opacity-80 hover:opacity-100 transition-opacity"
          @click="nextImage(post)"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd" />
          </svg>
        </button>
      </div>
      <div v-if="post.type === 'video'" class="w-full h-full">
        <video
          :src="post.video"
          controls
          class="w-full h-full object-cover"
        ></video>
      </div>
    </div>

    <div class="p-3 sm:p-4">
      <div class="flex justify-between items-center mb-3">
        <div class="flex space-x-4">
          <button @click="toggleLike(post)" class="focus:outline-none">
            <HeartIcon
              :class="['h-6 w-6 cursor-pointer', post.liked ? 'text-red-500 fill-red-500' : 'text-white hover:text-gray-400']"
            />
          </button>
          <ChatBubbleLeftIcon class="h-6 w-6 text-white cursor-pointer hover:text-gray-400" />
          <PaperAirplaneIcon
            class="h-6 w-6 text-white cursor-pointer hover:text-gray-400 transform -rotate-45"
          />
        </div>
        <BookmarkIcon class="h-6 w-6 text-white cursor-pointer hover:text-gray-400" />
      </div>

      <p class="text-sm font-semibold mb-2">{{ post.likes }} likes</p>

      <p class="text-sm leading-tight mb-2">
        <span class="font-semibold cursor-pointer hover:underline">{{ post.user.username }}</span>
        {{ post.caption }}
      </p>

      <button v-if="post.comments.length > 2" class="text-gray-500 text-sm mb-2 hover:underline">
        View all {{ post.comments.length }} comments
      </button>

      <div class="space-y-1 mb-2">
        <div
          v-for="(comment, cIndex) in post.comments.slice(0, 2)"
          :key="cIndex"
          class="text-sm"
        >
          <span class="font-semibold cursor-pointer hover:underline">{{ comment.user }}</span>
          <span class="ml-1">{{ comment.text }}</span>
          <span v-if="comment.emoji" class="ml-1">{{ comment.emoji }}</span>
        </div>
      </div>

      <p class="text-gray-500 text-xs uppercase mb-4">{{ post.timeAgo }}</p>

      <div class="flex items-center border-t border-gray-800 pt-3 space-x-2">
        <FaceSmileIcon class="h-6 w-6 text-gray-400 cursor-pointer hover:text-white" />
        <input
          type="text"
          placeholder="Add a comment..."
          class="flex-grow bg-transparent text-white placeholder-gray-500 text-sm focus:outline-none"
        />
        <button class="text-blue-400 font-semibold text-sm ml-2 opacity-50 cursor-not-allowed">
          Post
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import {
  HeartIcon,
  ChatBubbleLeftIcon,
  PaperAirplaneIcon,
  EllipsisHorizontalIcon,
  CheckCircleIcon, // Using CheckCircleIcon for verified
  BookmarkIcon,
  FaceSmileIcon,
} from "@heroicons/vue/24/outline";
// Note: @iconify/vue is not needed if only using Heroicons
// import { Icon } from "@iconify/vue";
import { reactive, computed } from "vue";

const posts = reactive([
  {
    user: {
      username: "john_doe",
      avatar: "/images/john_doe.png",
      fullName: "John Doe",
      verified: true,
      posts: 150,
      followers: "3K",
      following: 500,
      recentPosts: ["/images/post-placeholder.png", "/images/post-placeholder1.png", "/images/post-placeholder2.png"],
      isFollowing: false, // Added for consistency with suggestions
    },
    type: "image",
    image: "/images/post-placeholder1.png",
    likes: 120,
    liked: false, // Set to false by default for better user interaction
    caption: "A beautiful sunset over the mountains. Nature's masterpiece! #sunset #nature #mountains",
    comments: [
      { user: "emily", text: "Stunning view!", emoji: "😍" },
      { user: "alex", text: "Where is this?", emoji: "📍" },
      { user: "sarah", text: "Looks peaceful.", emoji: "" },
    ],
    timeAgo: "2 HOURS AGO",
  },
  {
    user: {
      username: "emily",
      avatar: "/images/emily.png",
      fullName: "Emily Jones",
      verified: false,
      posts: 90,
      followers: "2K",
      following: 300,
      recentPosts: ["/images/emily.png", "/images/sarah.png"],
      isFollowing: false,
    },
    type: "video",
    video: "/videos/sample-video.mp4",
    likes: 85,
    liked: false,
    caption: "A beautiful sunset by the lake 🌅. So calming and serene. #lake #sunset #video",
    comments: [
      { user: "john_doe", text: "This looks amazing!", emoji: "🔥" },
      { user: "alex", text: "Love it!", emoji: "❤️" },
      { user: "david", text: "Great capture!" },
      { user: "mike", text: "So peaceful." },
    ],
    timeAgo: "1 DAY AGO",
  },
  {
    user: {
      username: "alex",
      avatar: "/images/alex.png",
      fullName: "Mark Jones",
      verified: true,
      posts: 200,
      followers: "5K",
      following: 700,
      recentPosts: ["/images/alex.png", "/images/italy.png", "/images/paris.png"],
      isFollowing: false,
    },
    type: "carousel",
    images: ["/images/paris.png", "/images/italy.png"],
    currentImageIndex: 0,
    likes: 190,
    liked: false,
    caption: "Traveling through Europe 🚆. Such incredible architecture and history! #travel #europe #paris #italy",
    comments: [
      { user: "emily", text: "So jealous!", emoji: "😍" },
      { user: "john_doe", text: "What a trip!", emoji: "✈️" },
      { user: "sarah", text: "Dream destination!" },
    ],
    timeAgo: "3 DAYS AGO",
  },
]);

// This computed property might not be necessary if you want to show all posts,
// but keeping it if the intention is to only show one post per unique user.
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

// Function to toggle follow status for a user object within the post's user data
const toggleUserFollow = (user) => {
  user.isFollowing = !user.isFollowing;
};
</script>

<style scoped>
/* No need for @import 'tailwindcss/tailwind.css'; if configured globally in nuxt.config.js */
/* No specific custom CSS needed here, Tailwind handles it */
</style>
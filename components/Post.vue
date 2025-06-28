<template>
 <div
  v-for="post in uniquePosts"
  :key="post.id"
  class="w-full bg-black text-white border border-gray-800 rounded-lg
         mb-4 sm:mb-6
         px-0
         max-w-[470px] mx-auto
         fade-in"
>
    <div class="relative flex items-center justify-between px-3 py-2 sm:px-4 sm:py-3">
    
      <div class="flex items-center space-x-3 group">
        <img
          :src="post.user.avatar"
          :alt="post.user.username"
          class="h-8 w-8 sm:h-9 sm:w-9 rounded-full border border-gray-700 cursor-pointer object-cover instagram-hover"
        />
        <div class="flex items-center space-x-1">
          <a href="#" class="font-semibold text-sm hover:underline instagram-hover">
            {{ post.user.username }}
          </a>
          <svg
            v-if="post.user.verified"
            class="h-3.5 w-3.5 text-blue-500 flex-shrink-0"
            viewBox="0 0 24 24"
            fill="currentColor"
          >
            <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
          </svg>
          <span class="text-gray-500 text-xs">• {{ post.timeAgo }}</span>
        </div>

        <div
          class="absolute left-0 top-10 w-[340px] bg-black text-white border border-gray-700
                 rounded-lg p-4 shadow-lg hidden group-hover:flex flex-col space-y-4 z-20
                 instagram-shadow-lg"
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
                <svg
                  v-if="post.user.verified"
                  class="h-5 w-5 text-blue-500"
                  viewBox="0 0 24 24"
                  fill="currentColor"
                >
                  <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
                </svg>
              </div>
              <p class="text-gray-400 text-sm truncate">{{ post.user.fullName }}</p>
            </div>
          </div>
          <div class="flex justify-between text-sm text-gray-400">
            <div class="flex flex-col items-center">
              <p class="font-bold text-white">{{ post.user.posts }}</p><p>posts</p>
            </div>
            <div class="flex flex-col items-center">
              <p class="font-bold text-white">{{ post.user.followers }}</p><p>followers</p>
            </div>
            <div class="flex flex-col items-center">
              <p class="font-bold text-white">{{ post.user.following }}</p><p>following</p>
            </div>
          </div>
          <div class="grid grid-cols-3 gap-1">
            <img
              v-for="(img, i) in post.user.recentPosts.slice(0,3)"
              :key="i"
              :src="img"
              :alt="'Recent post '+(i+1)"
              class="h-20 w-full object-cover rounded"
            />
          </div>
          <button
            @click.stop="toggleUserFollow(post.user)"
            :class="isFollowingThisUser[post.user.username]
                    ? 'bg-gray-700 hover:bg-gray-600'
                    : 'bg-blue-500 hover:bg-blue-600'"
            class="w-full text-sm font-medium py-2 rounded text-white transition-colors instagram-hover"
          >
            {{ isFollowingThisUser[post.user.username] ? 'Following' : 'Follow' }}
          </button>
        </div>
      </div>
      <svg class="h-6 w-6 text-gray-400 hover:text-white cursor-pointer instagram-hover" fill="currentColor" viewBox="0 0 24 24">
        <path d="M12 8c1.1 0 2-.9 2-2s-.9-2-2-2-2 .9-2 2 .9 2 2 2zm0 2c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2zm0 6c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/>
      </svg>
    </div>

<div class="relative w-full aspect-square border-t border-gray-800">
  <template v-if="post.type==='image'">
    <img :src="post.image" :alt="post.caption" class="w-full h-full object-cover" />
  </template>
      <template v-else-if="post.type==='carousel'">
        <img
          :src="post.images[post.currentImageIndex]"
          class="w-full h-full object-cover"
        />
        <div class="absolute bottom-2 left-1/2 -translate-x-1/2 flex space-x-1">
          <span
            v-for="(_, idx) in post.images"
            :key="idx"
            :class="[
              'h-1.5 w-1.5 rounded-full transition-colors',
              post.currentImageIndex===idx
                ? 'bg-blue-500'
                : 'bg-gray-400 opacity-50'
            ]"
          />
        </div>
        <button
          v-if="post.currentImageIndex>0"
          @click="prevImage(post)"
          class="absolute left-2 top-1/2 -translate-y-1/2 bg-black/60 p-1 rounded-full opacity-80 hover:opacity-100 instagram-hover"
        >
          ‹
        </button>
        <button
          v-if="post.currentImageIndex<post.images.length-1"
          @click="nextImage(post)"
          class="absolute right-2 top-1/2 -translate-y-1/2 bg-black/60 p-1 rounded-full opacity-80 hover:opacity-100 instagram-hover"
        >
          ›
        </button>
      </template>
      <template v-else-if="post.type==='video'">
        <video :src="post.video" controls class="w-full h-full object-cover" />
      </template>
    </div>

    <div class="px-3 py-2 sm:px-4 sm:py-3">
      <div class="flex justify-between items-center mb-3">
        <div class="flex space-x-4">
          <button @click="toggleLike(post)" class="focus:outline-none instagram-hover">
            <svg
              v-if="post.liked"
              class="h-6 w-6 text-red-500 cursor-pointer transition-colors heart-animation"
              fill="currentColor"
              viewBox="0 0 24 24"
            >
              <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
            </svg>
            <svg
              v-else
              class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer transition-colors"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              stroke-width="2"
            >
              <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
            </svg>
          </button>
          <svg class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer instagram-hover" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
            <path d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"/>
          </svg>
          <svg class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer instagram-hover transform -rotate-45" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
            <path d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"/>
          </svg>
        </div>
        <svg class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer instagram-hover" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
          <path d="M5 5a2 2 0 012-2h10a2 2 0 012 2v16l-7-3.5L5 21V5z"/>
        </svg>
      </div>

      <p class="text-sm font-semibold mb-2">{{ post.likes.toLocaleString() }} likes</p>

      <p class="text-sm leading-tight mb-2">
        <span class="font-semibold hover:underline cursor-pointer instagram-hover">{{ post.user.username }}</span>
        <span v-if="!localShowFullCaption[post.id]">
          {{ post.caption.slice(0,100) }}
          <span
            v-if="post.caption.length>100"
            class="text-gray-500 cursor-pointer instagram-hover"
            @click="localShowFullCaption[post.id]=true"
          >... more</span>
        </span>
        <span v-else>{{ post.caption }}</span>
        <a href="#" class="text-gray-500 text-xs ml-2 hover:underline instagram-hover">See translation</a>
      </p>

      <button
        v-if="post.comments.length>2"
        class="text-gray-500 text-sm mb-2 hover:underline instagram-hover"
      >View all {{ post.comments.length }} comments</button>

      <div class="space-y-1 mb-2">
        <div
          v-for="(c, i) in post.comments.slice(0,2)"
          :key="i"
          class="text-sm"
        >
          <span class="font-semibold hover:underline cursor-pointer instagram-hover">{{ c.user }}</span>
          <span class="ml-1">{{ c.text }}</span>
          <span v-if="c.emoji" class="ml-1">{{ c.emoji }}</span>
        </div>
      </div>

      <p class="text-gray-500 text-xs uppercase mb-4">{{ post.timeAgo }}</p>

      <div class="flex items-center border-t border-gray-800 pt-3 space-x-2">
        <svg class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer instagram-hover" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
          <path d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
        </svg>
        <input
          type="text"
          v-model="localNewComment[post.id]"
          :placeholder="'Add a comment as ' + currentUser.username + '...'"
          class="flex-grow bg-transparent placeholder-gray-500 text-sm focus:outline-none"
        />
        <button
          :disabled="!localNewComment[post.id]?.trim()"
          :class="{
            'text-blue-400': localNewComment[post.id]?.trim(),
            'opacity-50 cursor-not-allowed': !localNewComment[post.id]?.trim()
          }"
          class="font-semibold text-sm ml-2 transition-opacity instagram-hover"
          @click="addComment(post.id)"
        >Post</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, computed, ref } from 'vue'

const posts = reactive([
  {
    id: 1, // Added ID for easier local state management
    user: {
      username: "john_doe",
      avatar: "/images/john_doe.png",
      fullName: "John Doe",
      verified: true,
      posts: 150,
      followers: "3K",
      following: 500, // Original 'following' property
      recentPosts: ["/images/post-placeholder.png", "/images/post-placeholder1.png", "/images/post-placeholder2.png"],
    },
    type: "image",
    image: "/images/post-placeholder1.png",
    likes: 120, // Original numeric likes
    liked: false,
    caption: "A beautiful sunset over the mountains. Nature's masterpiece! #sunset #nature #mountains. This is a very long caption to demonstrate the 'more' functionality, as it often appears on Instagram posts. It needs to be long enough to be truncated. Keep going, this is just to fill space.",
    comments: [
      { user: "emily", text: "Stunning view!", emoji: "😍" },
      { user: "alex", text: "Where is this?", emoji: "📍" },
      { user: "sarah", text: "Looks peaceful.", emoji: "" },
      { user: "david", text: "Incredible shot!", emoji: "" },
      { user: "olivia", text: "Must visit!", emoji: "🤩" },
    ],
    timeAgo: "2hr",
    currentImageIndex: 0, // for carousel type only
  },
  {
    id: 2,
    user: {
      username: "emily_travels", // Adjusted username to avoid conflict with `emily` from suggestions
      avatar: "/images/emily.png",
      fullName: "Emily Jones",
      verified: false,
      posts: 90,
      followers: "2K",
      following: 300,
      recentPosts: ["/images/emily.png", "/images/sarah.png"],
    },
    type: "video",
    video: "/videos/sample-video.mp4",
    likes: 85,
    liked: false,
    caption: "A beautiful sunset by the lake 🌅. So calming and serene. #lake #sunset #video",
    comments: [
      { user: "john_doe", text: "This looks amazing!", emoji: "🔥" },
      { user: "alex_adventures", text: "Love it!", emoji: "❤️" },
      { user: "david", text: "Great capture!" },
      { user: "mike", text: "So peaceful." },
    ],
    timeAgo: "1d",
    currentImageIndex: 0,
  },
  {
    id: 3,
    user: {
      username: "alex_captures", // Adjusted username
      avatar: "/images/alex.png",
      fullName: "Mark Jones",
      verified: true,
      posts: 200,
      followers: "5K",
      following: 700,
      recentPosts: ["/images/paris.png", "/images/italy.png", "/images/post-placeholder.png"], // Corrected image paths
    },
    type: "carousel",
    images: ["/images/paris.png", "/images/italy.png", "/images/post-placeholder.png"],
    currentImageIndex: 0,
    likes: 190,
    liked: false,
    caption: "Traveling through Europe 🚆. Such incredible architecture and history! #travel #europe #paris #italy #adventure #wanderlust. Another fairly long caption to showcase the 'more' functionality on a carousel post. Europe is full of wonders!",
    comments: [
      { user: "emily_travels", text: "So jealous!", emoji: "😍" },
      { user: "john_doe", text: "What a trip!", emoji: "✈️" },
      { user: "globetrotter", text: "Dream destination!" },
      { user: "culture_lover", text: "Paris is always a good idea." },
    ],
    timeAgo: "3d",
  },
]);

const localShowFullCaption = ref({})
const localNewComment = ref({})
const isFollowingThisUser = ref({})
const currentUser = { username: 'cdjkr', avatar: '/images/profile.png' }

const uniquePosts = computed(() => {
  const seen = new Set()
  return posts.filter(p => {
    if (seen.has(p.user.username)) return false
    seen.add(p.user.username)
    return true
  })
})

const toggleLike = post => {
  post.liked = !post.liked
  post.likes += post.liked ? 1 : -1
}
const nextImage = post => {
  post.currentImageIndex = (post.currentImageIndex + 1) % post.images.length
}
const prevImage = post => {
  post.currentImageIndex = (post.currentImageIndex - 1 + post.images.length) % post.images.length
}
const toggleUserFollow = user => {
  if (typeof isFollowingThisUser.value[user.username] === 'undefined') {
    isFollowingThisUser.value[user.username] = false
  }
  isFollowingThisUser.value[user.username] = !isFollowingThisUser.value[user.username]
}
const addComment = postId => {
  const post = posts.find(p => p.id === postId)
  const txt = localNewComment.value[postId]?.trim()
  if (post && txt) {
    post.comments.push({ user: currentUser.username, text: txt, emoji: '' })
    localNewComment.value[postId] = ''
  }
}
</script>

<style scoped>
/* No extra CSS—Tailwind handles it all */
</style>
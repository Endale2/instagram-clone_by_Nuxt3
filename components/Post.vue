<template>
  <div
    v-for="post in uniquePosts"
    :key="post.id"
    class="w-full bg-black text-white border border-gray-800 rounded-lg
           mb-4 sm:mb-6
           px-0
           sm:max-w-[470px] sm:mx-auto
           md:px-4 lg:px-6"
  >
    <!-- Post Header -->
    <div class="relative flex items-center justify-between px-3 py-2 sm:px-4 sm:py-3">
      <div class="flex items-center space-x-3 group">
        <img
          :src="post.user.avatar"
          :alt="post.user.username"
          class="h-9 w-9 rounded-full border border-gray-700 object-cover cursor-pointer"
        />
        <div class="flex items-center space-x-1">
          <a href="#" class="font-semibold text-sm hover:underline">
            {{ post.user.username }}
          </a>
          <CheckCircleIcon
            v-if="post.user.verified"
            class="h-4 w-4 text-blue-500"
          />
          <span class="text-gray-500 text-xs">• {{ post.timeAgo }}</span>
        </div>
      </div>
      <EllipsisHorizontalIcon class="h-6 w-6 text-gray-400 hover:text-white cursor-pointer" />
    </div>

    <!-- Media Content (Square) -->
    <div class="relative w-full aspect-square border-t border-gray-800">
      <template v-if="post.type === 'image'">
        <img :src="post.image" :alt="post.caption" class="w-full h-full object-cover" />
      </template>

      <template v-else-if="post.type === 'carousel'">
        <img
          :src="post.images[post.currentImageIndex]"
          class="w-full h-full object-cover"
        />
        <!-- Carousel Dots -->
        <div class="absolute bottom-2 left-1/2 -translate-x-1/2 flex space-x-1">
          <span
            v-for="(_, i) in post.images"
            :key="i"
            :class="[
              'h-1.5 w-1.5 rounded-full',
              post.currentImageIndex === i ? 'bg-white' : 'bg-gray-500 opacity-50'
            ]"
          />
        </div>
        <!-- Arrows -->
        <button
          v-if="post.currentImageIndex > 0"
          @click="prevImage(post)"
          class="absolute left-2 top-1/2 -translate-y-1/2 bg-black/60 p-1 rounded-full text-white"
        >‹</button>
        <button
          v-if="post.currentImageIndex < post.images.length - 1"
          @click="nextImage(post)"
          class="absolute right-2 top-1/2 -translate-y-1/2 bg-black/60 p-1 rounded-full text-white"
        >›</button>
      </template>

      <template v-else-if="post.type === 'video'">
        <video :src="post.video" controls class="w-full h-full object-cover" />
      </template>
    </div>

    <!-- Post Actions & Comments -->
    <div class="px-3 py-2 sm:px-4 sm:py-3">
      <!-- Like/Comment/Share/Save -->
      <div class="flex justify-between items-center mb-3">
        <div class="flex space-x-4">
          <button @click="toggleLike(post)" class="focus:outline-none">
            <component
              :is="post.liked ? HeartSolid : HeartOutline"
              :class="[
                'h-6 w-6 transition-colors',
                post.liked ? 'text-red-500' : 'text-white hover:text-gray-400'
              ]"
            />
          </button>
          <ChatBubbleLeftIcon class="h-6 w-6 hover:text-gray-400 cursor-pointer" />
          <PaperAirplaneIcon class="h-6 w-6 -rotate-45 hover:text-gray-400 cursor-pointer" />
        </div>
        <BookmarkIcon class="h-6 w-6 hover:text-gray-400 cursor-pointer" />
      </div>

      <!-- Like Count -->
      <p class="text-sm font-semibold mb-2">
        {{ post.likes.toLocaleString() }} likes
      </p>

      <!-- Caption -->
      <p class="text-sm mb-2 leading-tight">
        <span class="font-semibold hover:underline cursor-pointer">{{ post.user.username }}</span>
        <span v-if="!localShowFullCaption[post.id]">
          {{ post.caption.slice(0, 100) }}
          <span
            v-if="post.caption.length > 100"
            class="text-gray-500 cursor-pointer"
            @click="localShowFullCaption[post.id] = true"
          >... more</span>
        </span>
        <span v-else>{{ post.caption }}</span>
        <span class="text-gray-500 text-xs ml-2 hover:underline">See translation</span>
      </p>

      <!-- Comments Preview -->
      <button
        v-if="post.comments.length > 2"
        class="text-gray-500 text-sm mb-2 hover:underline"
      >View all {{ post.comments.length }} comments</button>

      <div class="space-y-1 mb-2">
        <div
          v-for="(comment, i) in post.comments.slice(0, 2)"
          :key="i"
          class="text-sm"
        >
          <span class="font-semibold hover:underline cursor-pointer">{{ comment.user }}</span>
          <span class="ml-1">{{ comment.text }}</span>
          <span v-if="comment.emoji" class="ml-1">{{ comment.emoji }}</span>
        </div>
      </div>

      <p class="text-gray-500 text-xs uppercase mb-4">{{ post.timeAgo }}</p>

      <!-- Comment Input -->
      <div class="flex items-center border-t border-gray-800 pt-3 space-x-2">
        <FaceSmileIcon class="h-6 w-6 hover:text-white cursor-pointer" />
        <input
          v-model="localNewComment[post.id]"
          :placeholder="'Add a comment as ' + currentUser.username + '...'"
          class="flex-grow bg-transparent placeholder-gray-500 text-sm focus:outline-none"
        />
        <button
          @click="addComment(post.id)"
          :disabled="!localNewComment[post.id]?.trim()"
          class="font-semibold text-sm text-blue-400 disabled:opacity-50 disabled:cursor-not-allowed"
        >Post</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref, computed } from 'vue'
import {
  HeartIcon as HeartOutline,
  ChatBubbleLeftIcon,
  PaperAirplaneIcon,
  EllipsisHorizontalIcon,
  CheckCircleIcon,
  BookmarkIcon,
  FaceSmileIcon
} from '@heroicons/vue/24/outline'
import { HeartIcon as HeartSolid } from '@heroicons/vue/24/solid'

const currentUser = { username: 'cdjkr', avatar: '/images/profile.png' }

const posts = reactive([
  {
    id: 1,
    user: {
      username: "john_doe",
      fullName: "John Doe",
      verified: true,
      avatar: "/images/john_doe.png",
      posts: 123,
      followers: "4K",
      following: 150,
      recentPosts: ["/images/post-placeholder.png"]
    },
    type: "image",
    image: "/images/post-placeholder.png",
    caption: "A beautiful mountain sunset #travel #sunset 🌄",
    liked: false,
    likes: 192,
    comments: [
      { user: "alex", text: "Amazing!", emoji: "🔥" },
      { user: "sarah", text: "Where is this?" }
    ],
    timeAgo: "3h",
    currentImageIndex: 0,
  },
  {
    id: 2,
    user: {
      username: "alex_travels",
      fullName: "Alex Brown",
      verified: false,
      avatar: "/images/alex.png",
      posts: 99,
      followers: "12K",
      following: 300,
      recentPosts: ["/images/alex.png"]
    },
    type: "carousel",
    images: ["/images/post-placeholder1.png", "/images/post-placeholder2.png"],
    caption: "Exploring new places 🚶‍♂️",
    liked: false,
    likes: 324,
    comments: [],
    timeAgo: "1d",
    currentImageIndex: 0
  },
  {
    id: 3,
    user: {
      username: "emily_vibes",
      fullName: "Emily Rose",
      verified: false,
      avatar: "/images/emily.png",
      posts: 200,
      followers: "18K",
      following: 800,
      recentPosts: ["/images/sarah.png"]
    },
    type: "video",
    video: "/videos/sample-video.mp4",
    caption: "This sunset video is unreal 😍 #nature",
    liked: false,
    likes: 442,
    comments: [],
    timeAgo: "2d",
    currentImageIndex: 0
  }
])

const localShowFullCaption = ref({})
const localNewComment = ref({})
const isFollowingThisUser = ref({})

const uniquePosts = computed(() => {
  const seen = new Set()
  return posts.filter(post => {
    if (seen.has(post.user.username)) return false
    seen.add(post.user.username)
    return true
  })
})

function toggleLike(post) {
  post.liked = !post.liked
  post.likes += post.liked ? 1 : -1
}

function nextImage(post) {
  post.currentImageIndex = (post.currentImageIndex + 1) % post.images.length
}

function prevImage(post) {
  post.currentImageIndex =
    (post.currentImageIndex - 1 + post.images.length) % post.images.length
}

function addComment(postId) {
  const post = posts.find(p => p.id === postId)
  const text = localNewComment.value[postId]?.trim()
  if (text) {
    post.comments.push({ user: currentUser.username, text, emoji: '' })
    localNewComment.value[postId] = ''
  }
}
</script>

<style scoped>
/* No extra CSS—Tailwind handles it all */
</style>
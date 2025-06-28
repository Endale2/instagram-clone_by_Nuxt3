<template>
 <div
  v-for="post in uniquePosts"
  :key="post.id"
  class="w-full bg-black text-white border border-gray-800 rounded-lg
         mb-4 sm:mb-6
         px-0
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
      <MoreHorizontal class="h-6 w-6 text-gray-400 hover:text-white cursor-pointer instagram-hover" />
    </div>

<div class="relative w-full aspect-square border-t border-gray-800">
  <template v-if="post.type==='image'">
    <div 
      class="relative w-full h-full"
      @dblclick="handleDoubleClick(post)"
    >
      <img :src="post.image" :alt="post.caption" class="w-full h-full object-cover" />
      <!-- Double tap heart animation -->
      <div 
        v-if="post.showDoubleTapHeart"
        class="absolute inset-0 flex items-center justify-center pointer-events-none"
      >
        <Heart class="h-24 w-24 text-red-500 animate-ping" fill="currentColor" />
      </div>
    </div>
  </template>
      <template v-else-if="post.type==='carousel'">
        <div class="relative w-full h-full">
          <div 
            @dblclick="handleDoubleClick(post)"
            class="relative w-full h-full"
          >
            <img
              :src="post.images[post.currentImageIndex]"
              class="w-full h-full object-cover"
            />
            <!-- Double tap heart animation -->
            <div 
              v-if="post.showDoubleTapHeart"
              class="absolute inset-0 flex items-center justify-center pointer-events-none"
            >
              <Heart class="h-24 w-24 text-red-500 animate-ping" fill="currentColor" />
            </div>
          </div>
          <!-- Carousel Dots -->
          <div class="absolute top-3 left-1/2 -translate-x-1/2 flex space-x-1">
            <span
              v-for="(_, idx) in post.images"
              :key="idx"
              :class="[
                'h-1.5 w-1.5 rounded-full transition-colors',
                post.currentImageIndex===idx
                  ? 'bg-white'
                  : 'bg-white/50'
              ]"
            />
          </div>
          <!-- Navigation Buttons -->
          <button
            v-if="post.currentImageIndex>0"
            @click="prevImage(post)"
            class="absolute left-2 top-1/2 -translate-y-1/2 bg-black/60 p-2 rounded-full opacity-80 hover:opacity-100 instagram-hover"
          >
            <ChevronLeft class="h-5 w-5 text-white" />
          </button>
          <button
            v-if="post.currentImageIndex<post.images.length-1"
            @click="nextImage(post)"
            class="absolute right-2 top-1/2 -translate-y-1/2 bg-black/60 p-2 rounded-full opacity-80 hover:opacity-100 instagram-hover"
          >
            <ChevronRight class="h-5 w-5 text-white" />
          </button>
        </div>
      </template>
      <template v-else-if="post.type==='video'">
        <div class="relative w-full h-full">
          <video 
            :src="post.video" 
            :ref="el => { if (el) videoRefs[post.id] = el }"
            class="w-full h-full object-cover"
            @click="toggleVideoPlay(post.id)"
            @timeupdate="updateVideoProgress(post.id)"
            @ended="onVideoEnd(post.id)"
            @loadedmetadata="onVideoLoad(post.id)"
            preload="metadata"
            muted
          />
          <!-- Video Play Button Overlay -->
          <div 
            v-if="!post.isPlaying" 
            @click="toggleVideoPlay(post.id)"
            class="absolute inset-0 flex items-center justify-center bg-black/30 cursor-pointer"
          >
            <Play class="h-16 w-16 text-white opacity-80" />
          </div>
          <!-- Video Progress Bar -->
          <div class="absolute bottom-0 left-0 right-0 h-1 bg-black/50">
            <div 
              class="h-full bg-white transition-all duration-100"
              :style="{ width: post.videoProgress + '%' }"
            ></div>
          </div>
          <!-- Video Duration -->
          <div class="absolute top-3 right-3 bg-black/60 px-2 py-1 rounded text-white text-xs">
            {{ formatTime(post.videoDuration) }}
          </div>
        </div>
      </template>
    </div>

    <div class="px-3 py-2 sm:px-4 sm:py-3">
      <div class="flex justify-between items-center mb-3">
        <div class="flex space-x-4">
          <button @click="toggleLike(post)" class="focus:outline-none instagram-hover">
            <Heart
              v-if="post.liked"
              class="h-6 w-6 text-red-500 cursor-pointer transition-colors heart-animation"
              fill="currentColor"
            />
            <Heart
              v-else
              class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer transition-colors"
            />
          </button>
          <MessageCircle class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer instagram-hover" />
          <Send class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer instagram-hover transform -rotate-45" />
        </div>
        <Bookmark class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer instagram-hover" />
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
        <Smile class="h-6 w-6 text-white hover:text-gray-400 cursor-pointer instagram-hover" />
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
import { reactive, computed, ref, onMounted } from 'vue'
import { 
  Heart, 
  MessageCircle, 
  Send, 
  Bookmark, 
  Smile, 
  MoreHorizontal,
  ChevronLeft,
  ChevronRight,
  Play
} from 'lucide-vue-next'

const posts = reactive([
  {
    id: 1,
    user: {
      username: "john_doe",
      avatar: "/images/john_doe.png",
      fullName: "John Doe",
      verified: true,
      posts: 150,
      followers: "3K",
      following: 500,
      recentPosts: ["/images/post-placeholder.png", "/images/post-placeholder1.png", "/images/post-placeholder2.png"],
    },
    type: "image",
    image: "/images/post-placeholder1.png",
    likes: 120,
    liked: false,
    showDoubleTapHeart: false,
    caption: "A beautiful sunset over the mountains. Nature's masterpiece! #sunset #nature #mountains. This is a very long caption to demonstrate the 'more' functionality, as it often appears on Instagram posts. It needs to be long enough to be truncated. Keep going, this is just to fill space.",
    comments: [
      { user: "emily", text: "Stunning view!", emoji: "😍" },
      { user: "alex", text: "Where is this?", emoji: "📍" },
      { user: "sarah", text: "Looks peaceful.", emoji: "" },
      { user: "david", text: "Incredible shot!", emoji: "" },
      { user: "olivia", text: "Must visit!", emoji: "🤩" },
    ],
    timeAgo: "2hr",
    currentImageIndex: 0,
  },
  {
    id: 2,
    user: {
      username: "emily_travels",
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
    isPlaying: false,
    videoProgress: 0,
    videoDuration: 0,
    showDoubleTapHeart: false,
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
      username: "alex_captures",
      avatar: "/images/alex.png",
      fullName: "Mark Jones",
      verified: true,
      posts: 200,
      followers: "5K",
      following: 700,
      recentPosts: ["/images/paris.png", "/images/italy.png", "/images/post-placeholder.png"],
    },
    type: "carousel",
    images: ["/images/paris.png", "/images/italy.png", "/images/post-placeholder.png"],
    currentImageIndex: 0,
    likes: 190,
    liked: false,
    showDoubleTapHeart: false,
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
const videoRefs = ref({})
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

const toggleVideoPlay = (postId) => {
  const post = posts.find(p => p.id === postId)
  const video = videoRefs.value[postId]
  
  if (video) {
    if (post.isPlaying) {
      video.pause()
      post.isPlaying = false
    } else {
      video.play().catch(err => {
        console.log('Video play failed:', err)
        // Fallback: try to play without user interaction
        video.muted = true
        video.play()
      })
      post.isPlaying = true
    }
  }
}

const updateVideoProgress = (postId) => {
  const post = posts.find(p => p.id === postId)
  const video = videoRefs.value[postId]
  
  if (video && !video.paused) {
    post.videoProgress = (video.currentTime / video.duration) * 100
  }
}

const onVideoEnd = (postId) => {
  const post = posts.find(p => p.id === postId)
  post.isPlaying = false
  post.videoProgress = 0
}

const onVideoLoad = (postId) => {
  const post = posts.find(p => p.id === postId)
  const video = videoRefs.value[postId]
  if (video) {
    post.videoDuration = video.duration
  }
}

const handleDoubleClick = (post) => {
  if (!post.liked) {
    post.liked = true
    post.likes += 1
  }
  post.showDoubleTapHeart = true
  setTimeout(() => {
    post.showDoubleTapHeart = false
  }, 1000)
}

const formatTime = (seconds) => {
  if (!seconds) return '0:00'
  const mins = Math.floor(seconds / 60)
  const secs = Math.floor(seconds % 60)
  return `${mins}:${secs.toString().padStart(2, '0')}`
}

onMounted(() => {
  // Initialize video progress for all video posts
  posts.forEach(post => {
    if (post.type === 'video') {
      post.videoProgress = 0
      post.isPlaying = false
      post.videoDuration = 0
    }
    post.showDoubleTapHeart = false
  })
})
</script>

<style scoped>
/* No extra CSS—Tailwind handles it all */
</style>
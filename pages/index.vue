<template>
  <div class="flex bg-black text-white min-h-screen">
    <!-- Sidebar -->
    <Sidebar />

    <!-- Main Content Wrapper -->
    <div class="ml-64 flex-grow flex py-4 px-6 max-w-[1200px] mx-auto">
      <!-- Main Content Section -->
      <div class="flex-grow max-w-[600px] pr-6">
        <!-- Stories Section -->
        <div class="pb-4 border-b border-gray-700">
          <Stories />
        </div>

        <!-- Posts Section -->
        <section class="mt-6 space-y-6">
          <Post  />
        </section>
      </div>

      <!-- Vertical Separator -->
      <div class="w-[1px] bg-gray-700 flex-shrink-0"></div>

      <!-- Suggestions Section -->
      <div class="w-[320px] flex-shrink-0 pl-6">
        <Suggestions />
      </div>
    </div>
  </div>
</template>

<script setup>
import Sidebar from "~/components/Sidebar.vue";
import Stories from "~/components/Stories.vue";
import Post from "~/components/Post.vue";
import Suggestions from "~/components/Suggestions.vue";
</script>

<style scoped>
@import 'tailwindcss/tailwind.css';

/* Prevent horizontal scrolling */
body {
  overflow-x: hidden;
}

/* Fine-tune spacing */
.pr-6 {
  padding-right: 1.5rem; /* Adjust spacing between main content and separator */
}
.pl-6 {
  padding-left: 1.5rem; /* Adjust spacing for suggestions section */
}
</style>
<template>
  <div class="flex bg-black text-white min-h-screen">
    <div
      class="flex-1 py-4 px-4 sm:px-6 md:max-w-screen-lg mx-auto lg:max-w-[1200px] flex flex-col md:flex-row"
    >
      <div class="flex-grow md:max-w-[600px] md:pr-6">
        <div class="pb-4 border-b border-gray-700">
          <Stories />
        </div>

        <section class="mt-6 space-y-6">
          <Post />
        </section>
      </div>

      <div class="hidden md:block w-[1px] bg-gray-700 flex-shrink-0 mx-6"></div>

      <div class="hidden md:block w-[320px] flex-shrink-0 pl-6">
        <Suggestions />
      </div>
    </div>
  </div>
</template>

<script setup>
// We don't need to import Sidebar here since it's in the layout
import Stories from "~/components/Stories.vue";
import Post from "~/components/Post.vue";
import Suggestions from "~/components/Suggestions.vue";
</script>

<style scoped>
/* No additional styles needed here. Tailwind handles the responsiveness. */
</style>
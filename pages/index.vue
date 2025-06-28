<template>
  <div class="flex flex-col w-full">
    <!-- Stories & Posts -->
    <div class="flex-grow flex flex-col w-full">
      <Stories />
      <section class="space-y-4 sm:space-y-6 mt-6">
        <Post />
      </section>
    </div>

    <!-- Suggestions (Hidden on small screens) -->
    <div class="hidden lg:block fixed top-0 right-0 w-[320px] h-screen pt-8 z-10">
      <Suggestions />
    </div>
  </div>
</template>

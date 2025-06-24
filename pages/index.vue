<template>
  <div class="flex bg-black text-white min-h-screen">
    <div
      class="flex-1 max-w-screen-xl mx-auto
             flex flex-col md:flex-row md:items-start md:justify-between
             px-0 sm:px-4 md:px-6 py-4 md:gap-x-6"
    >
      <!-- Stories & Posts -->
      <div class="flex-grow flex flex-col max-w-full md:max-w-[calc(100%-370px)]">
        <Stories />
        <section class="space-y-4 sm:space-y-6 mt-6">
          <Post />
        </section>
      </div>

      <!-- Suggestions -->
      <Suggestions />
    </div>
  </div>
</template>

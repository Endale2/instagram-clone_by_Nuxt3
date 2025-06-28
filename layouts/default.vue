<template>
  <div class="bg-black min-h-screen text-white flex flex-col md:flex-row overflow-x-hidden">
    <!-- Mobile Header -->
    <AppHeader class="md:hidden" />

    <!-- Desktop Sidebar -->
    <Sidebar class="hidden md:block" />

    <!-- Main Content -->
    <div
      class="flex-1 w-full
             pt-[3.5rem] pb-[3.5rem] sm:pt-[4rem] sm:pb-[4rem]
             md:pt-0 md:pb-0
             md:ml-20 lg:ml-64
             overflow-x-hidden
             flex justify-center
             lg:mr-[320px]"
    >
      <!-- Content wrapper with max width like Instagram -->
      <div class="w-full max-w-[630px]">
        <NuxtPage />
      </div>
    </div>

    <!-- Mobile Footer -->
    <AppFooterMobile class="md:hidden" />
  </div>
</template>

<template>
  <div class="instagram-logo">
    <span class="logo-text">Instagram Clone</span>
  </div>
</template>

<script setup>
// No props or logic needed
</script>

<style scoped>
.instagram-logo {
  display: flex;
  align-items: center;
  justify-content: center;
}

.logo-text {
  font-family: 'Instagram Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
  font-weight: 600;
  font-size: 1.5rem;
  background: linear-gradient(45deg, #f09433 0%, #e6683c 25%, #dc2743 50%, #cc2366 75%, #bc1888 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  letter-spacing: -0.5px;
}

@media (max-width: 768px) {
  .logo-text {
    font-size: 1.25rem;
  }
}
</style> 
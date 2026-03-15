<template>
  <header class="sticky top-0 z-50 bg-white/90 backdrop-blur-sm border-b border-gray-100 shadow-sm">
    <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        <!-- Logo / Site Name -->
        <NuxtLink to="/" class="flex items-center gap-2 group">
          <span class="text-2xl">📝</span>
          <span class="font-bold text-gray-900 text-lg group-hover:text-primary-600 transition-colors">
            OJT Blog
          </span>
        </NuxtLink>

        <!-- Desktop Nav -->
        <nav class="hidden sm:flex items-center gap-1">
          <NuxtLink
            to="/"
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-primary-600 hover:bg-primary-50 transition-colors"
            active-class="text-primary-600 bg-primary-50"
            :exact="true"
          >
            Home
          </NuxtLink>
          <NuxtLink
            to="/blog"
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-primary-600 hover:bg-primary-50 transition-colors"
            active-class="text-primary-600 bg-primary-50"
          >
            Weekly Posts
          </NuxtLink>
          <NuxtLink
            to="/about"
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-primary-600 hover:bg-primary-50 transition-colors"
            active-class="text-primary-600 bg-primary-50"
          >
            About
          </NuxtLink>
        </nav>

        <!-- Mobile Menu Button -->
        <button
          class="sm:hidden p-2 rounded-lg text-gray-500 hover:text-primary-600 hover:bg-gray-100"
          aria-label="Toggle menu"
          @click="menuOpen = !menuOpen"
        >
          <svg v-if="!menuOpen" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
          <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>

      <!-- Mobile Nav -->
      <Transition name="slide-down">
        <nav v-if="menuOpen" class="sm:hidden pb-3 flex flex-col gap-1">
          <NuxtLink
            to="/"
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-primary-600 hover:bg-primary-50"
            active-class="text-primary-600 bg-primary-50"
            :exact="true"
            @click="menuOpen = false"
          >
            Home
          </NuxtLink>
          <NuxtLink
            to="/blog"
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-primary-600 hover:bg-primary-50"
            active-class="text-primary-600 bg-primary-50"
            @click="menuOpen = false"
          >
            Weekly Posts
          </NuxtLink>
          <NuxtLink
            to="/about"
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-primary-600 hover:bg-primary-50"
            active-class="text-primary-600 bg-primary-50"
            @click="menuOpen = false"
          >
            About
          </NuxtLink>
        </nav>
      </Transition>
    </div>
  </header>
</template>

<script setup>
const menuOpen = ref(false)
</script>

<style scoped>
.slide-down-enter-active,
.slide-down-leave-active {
  transition: all 0.2s ease;
}
.slide-down-enter-from,
.slide-down-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}
</style>

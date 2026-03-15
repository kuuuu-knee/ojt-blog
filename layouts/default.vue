<template>
  <div class="min-h-screen flex flex-col">
    <!-- Navigation -->
    <header class="bg-white border-b border-gray-100 sticky top-0 z-50 shadow-sm">
      <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center justify-between h-16">
          <!-- Logo / Brand -->
          <NuxtLink to="/" class="flex items-center gap-2 group">
            <span class="w-8 h-8 rounded-lg bg-brand-600 flex items-center justify-center text-white font-bold text-sm group-hover:bg-brand-700 transition-colors">
              OJT
            </span>
            <span class="font-semibold text-gray-900 hidden sm:block">My OJT Journey</span>
          </NuxtLink>

          <!-- Desktop Nav -->
          <nav class="hidden sm:flex items-center gap-1">
            <NuxtLink
              v-for="link in navLinks"
              :key="link.to"
              :to="link.to"
              class="px-4 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-brand-600 hover:bg-brand-50 transition-colors"
              active-class="text-brand-600 bg-brand-50"
            >
              {{ link.label }}
            </NuxtLink>
          </nav>

          <!-- Mobile Menu Button -->
          <button
            class="sm:hidden p-2 rounded-lg text-gray-500 hover:text-gray-700 hover:bg-gray-100"
            :aria-expanded="menuOpen"
            aria-label="Toggle navigation"
            @click="menuOpen = !menuOpen"
          >
            <svg v-if="!menuOpen" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
            <svg v-else class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>

        <!-- Mobile Nav -->
        <Transition
          enter-active-class="transition duration-150 ease-out"
          enter-from-class="opacity-0 -translate-y-1"
          enter-to-class="opacity-100 translate-y-0"
          leave-active-class="transition duration-100 ease-in"
          leave-from-class="opacity-100 translate-y-0"
          leave-to-class="opacity-0 -translate-y-1"
        >
          <nav v-if="menuOpen" class="sm:hidden pb-3 pt-1 border-t border-gray-100 mt-1">
            <NuxtLink
              v-for="link in navLinks"
              :key="link.to"
              :to="link.to"
              class="block px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-brand-600 hover:bg-brand-50"
              active-class="text-brand-600 bg-brand-50"
              @click="menuOpen = false"
            >
              {{ link.label }}
            </NuxtLink>
          </nav>
        </Transition>
      </div>
    </header>

    <!-- Page Content -->
    <main class="flex-1">
      <slot />
    </main>

    <!-- Footer -->
    <footer class="bg-white border-t border-gray-100 mt-16">
      <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <div class="flex flex-col sm:flex-row items-center justify-between gap-4">
          <div class="flex items-center gap-2 text-sm text-gray-500">
            <span class="w-6 h-6 rounded bg-brand-600 flex items-center justify-center text-white text-xs font-bold">OJT</span>
            <span>My OJT Journey — {{ new Date().getFullYear() }}</span>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
const menuOpen = ref(false)
const route = useRoute()

// Close mobile menu on route change
watch(() => route.path, () => { menuOpen.value = false })

const navLinks = [
  { to: '/', label: 'Home' },
  { to: '/blog', label: 'Blog' },
  { to: '/about', label: 'About' },
]
</script>

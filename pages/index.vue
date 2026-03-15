<template>
  <div>
    <!-- Hero Section -->
    <section class="bg-gradient-to-br from-primary-600 via-primary-700 to-primary-900 text-white py-20 px-4">
      <div class="max-w-4xl mx-auto text-center">
        <div class="inline-flex items-center gap-2 bg-white/10 backdrop-blur-sm px-4 py-1.5 rounded-full text-sm font-medium mb-6">
          <span class="w-2 h-2 bg-green-400 rounded-full animate-pulse" />
          Currently doing OJT
        </div>
        <h1 class="text-4xl sm:text-5xl font-extrabold tracking-tight mb-6 leading-tight">
          My OJT Journey 🚀
        </h1>
        <p class="text-lg sm:text-xl text-primary-100 max-w-2xl mx-auto mb-8">
          Welcome to my internship blog! Every week I document the tasks I work on,
          challenges I face, and lessons I learn during my On-the-Job Training.
        </p>
        <div class="flex flex-col sm:flex-row gap-3 justify-center">
          <NuxtLink to="/blog" class="btn-primary bg-white text-primary-700 hover:bg-primary-50">
            Read Weekly Posts
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
            </svg>
          </NuxtLink>
          <NuxtLink to="/about" class="btn-primary bg-primary-500/30 hover:bg-primary-500/50 border border-white/20">
            About Me
          </NuxtLink>
        </div>
      </div>
    </section>

    <!-- Stats Banner -->
    <section class="bg-white border-b border-gray-100">
      <div class="max-w-4xl mx-auto px-4 py-6 grid grid-cols-3 gap-4 text-center">
        <div>
          <p class="text-2xl font-bold text-primary-600">{{ posts.length }}</p>
          <p class="text-xs text-gray-500 mt-0.5">Weekly Posts</p>
        </div>
        <div>
          <p class="text-2xl font-bold text-primary-600">{{ totalWeeks }}</p>
          <p class="text-xs text-gray-500 mt-0.5">Weeks Completed</p>
        </div>
        <div>
          <p class="text-2xl font-bold text-primary-600">{{ totalImages }}</p>
          <p class="text-xs text-gray-500 mt-0.5">Photos Shared</p>
        </div>
      </div>
    </section>

    <!-- Recent Posts -->
    <section class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-14">
      <div class="flex items-center justify-between mb-8">
        <h2 class="text-2xl font-bold text-gray-900">Recent Updates</h2>
        <NuxtLink to="/blog" class="text-sm font-medium text-primary-600 hover:text-primary-800 flex items-center gap-1">
          All posts
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </NuxtLink>
      </div>

      <div v-if="posts.length" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <BlogCard v-for="post in posts" :key="post._path" :post="post" />
      </div>
      <p v-else class="text-gray-400 text-center py-12">No posts yet. Check back soon!</p>
    </section>

    <!-- About CTA -->
    <section class="bg-primary-50 border-t border-primary-100">
      <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-14 text-center">
        <h2 class="text-2xl font-bold text-gray-900 mb-3">About This Blog</h2>
        <p class="text-gray-600 max-w-xl mx-auto mb-6">
          This site is a digital journal of my internship experience. I post every week to keep
          track of my progress and share what I'm learning with friends, family, and future employers.
        </p>
        <NuxtLink to="/about" class="btn-primary">
          Learn More About Me
        </NuxtLink>
      </div>
    </section>
  </div>
</template>

<script setup>
const { data: posts } = await useAsyncData('recent-posts', () =>
  queryContent('posts').sort({ week: -1 }).limit(3).find()
)

const totalWeeks = computed(() => posts.value?.length ?? 0)
const totalImages = computed(() =>
  (posts.value ?? []).reduce((sum, p) => sum + (p.images?.length ?? 0), 0)
)
</script>

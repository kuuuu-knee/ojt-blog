<template>
  <NuxtLink :to="`/blog/${post._path.split('/').pop()}`" class="card group block">
    <!-- Cover image -->
    <div v-if="post.coverImage" class="aspect-video overflow-hidden bg-gray-100">
      <img
        :src="post.coverImage"
        :alt="post.title"
        class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300"
        loading="lazy"
      />
    </div>
    <!-- Fallback gradient banner -->
    <div v-else class="aspect-video bg-gradient-to-br from-primary-100 to-primary-200 flex items-center justify-center">
      <span class="text-4xl">📓</span>
    </div>

    <div class="p-5">
      <!-- Week badge + date -->
      <div class="flex items-center justify-between mb-3">
        <span class="badge-week">Week {{ post.week }}</span>
        <time class="text-xs text-gray-400 font-medium">{{ formatDate(post.date) }}</time>
      </div>

      <!-- Title -->
      <h2 class="font-bold text-gray-900 text-lg leading-snug mb-2 group-hover:text-primary-600 transition-colors line-clamp-2">
        {{ post.title }}
      </h2>

      <!-- Description -->
      <p v-if="post.description" class="text-sm text-gray-500 line-clamp-3 mb-4">
        {{ post.description }}
      </p>

      <!-- Read more -->
      <div class="flex items-center gap-1 text-sm font-medium text-primary-600 group-hover:gap-2 transition-all">
        Read more
        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
        </svg>
      </div>
    </div>
  </NuxtLink>
</template>

<script setup>
defineProps({
  post: {
    type: Object,
    required: true,
  },
})

function formatDate(dateStr) {
  if (!dateStr) return ''
  return new Date(dateStr).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  })
}
</script>

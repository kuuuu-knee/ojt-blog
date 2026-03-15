<template>
  <NuxtLink :to="post._path" class="card group flex flex-col overflow-hidden">
    <!-- Cover Image or Placeholder -->
    <div class="aspect-video bg-gradient-to-br from-brand-50 to-brand-100 overflow-hidden flex-shrink-0">
      <img
        v-if="post.coverImage"
        :src="post.coverImage"
        :alt="post.title"
        class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300"
        loading="lazy"
      >
      <div v-else class="w-full h-full flex items-center justify-center">
        <span class="text-5xl opacity-30 select-none">📋</span>
      </div>
    </div>

    <!-- Card Body -->
    <div class="p-5 flex flex-col flex-1">
      <div class="flex items-center gap-2 mb-3">
        <span class="badge bg-brand-100 text-brand-700">Week {{ post.week }}</span>
        <span class="text-xs text-gray-400">{{ post.date }}</span>
      </div>

      <h2 class="font-semibold text-gray-900 group-hover:text-brand-600 transition-colors line-clamp-2 mb-2 leading-snug">
        {{ post.title }}
      </h2>

      <p class="text-sm text-gray-500 line-clamp-3 flex-1">
        {{ post.description }}
      </p>

      <div v-if="post.tags?.length" class="flex flex-wrap gap-1.5 mt-4">
        <span
          v-for="tag in post.tags.slice(0, 3)"
          :key="tag"
          class="badge bg-gray-100 text-gray-600"
        >
          {{ tag }}
        </span>
      </div>

      <div class="flex items-center justify-between mt-4 pt-4 border-t border-gray-50">
        <span class="text-xs text-gray-400">
          {{ post.readTime ? `${post.readTime} min read` : 'Read more' }}
        </span>
        <span class="text-xs text-brand-600 font-medium group-hover:underline">Read →</span>
      </div>
    </div>
  </NuxtLink>
</template>

<script setup lang="ts">
defineProps<{
  post: Record<string, any>
}>()
</script>

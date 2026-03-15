<template>
  <div>
    <!-- Page Header -->
    <div class="bg-gradient-to-r from-brand-700 to-brand-500 text-white py-14">
      <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
        <span class="badge bg-white/20 text-white mb-3">📝 Weekly Updates</span>
        <h1 class="text-3xl sm:text-4xl font-bold font-serif mb-3">OJT Blog</h1>
        <p class="text-blue-100 max-w-xl">
          A running journal of my internship experience — tasks, challenges, lessons, and growth captured week by week.
        </p>
      </div>
    </div>

    <!-- Posts Grid -->
    <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
      <!-- Search / Filter Bar -->
      <div class="flex flex-col sm:flex-row gap-3 mb-10">
        <input
          v-model="search"
          type="text"
          placeholder="Search posts…"
          class="flex-1 px-4 py-2.5 rounded-lg border border-gray-200 text-sm focus:outline-none focus:ring-2 focus:ring-brand-400 bg-white"
        >
        <select
          v-model="sortOrder"
          class="px-4 py-2.5 rounded-lg border border-gray-200 text-sm focus:outline-none focus:ring-2 focus:ring-brand-400 bg-white"
        >
          <option value="newest">Newest First</option>
          <option value="oldest">Oldest First</option>
        </select>
      </div>

      <!-- Loading Skeletons -->
      <div v-if="pending" class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <div v-for="i in 6" :key="i" class="card p-6 animate-pulse">
          <div class="h-4 bg-gray-200 rounded w-1/4 mb-3" />
          <div class="h-6 bg-gray-200 rounded w-3/4 mb-2" />
          <div class="h-4 bg-gray-200 rounded w-full mb-1" />
          <div class="h-4 bg-gray-200 rounded w-5/6" />
        </div>
      </div>

      <!-- Empty State -->
      <div v-else-if="filteredPosts.length === 0" class="text-center py-20">
        <p class="text-4xl mb-4">🔍</p>
        <p class="text-gray-500">No posts found matching "<strong>{{ search }}</strong>"</p>
        <button class="mt-4 text-brand-600 hover:underline text-sm" @click="search = ''">Clear search</button>
      </div>

      <!-- Posts -->
      <div v-else class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <PostCard
          v-for="post in filteredPosts"
          :key="post._path"
          :post="post"
        />
      </div>

      <p v-if="!pending && filteredPosts.length > 0" class="text-xs text-gray-400 mt-8 text-center">
        Showing {{ filteredPosts.length }} post{{ filteredPosts.length !== 1 ? 's' : '' }}
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
useHead({ title: 'Blog — OJT Journey' })

const search = ref('')
const sortOrder = ref<'newest' | 'oldest'>('newest')

const { data: posts, pending } = await useAsyncData('blog-posts', () =>
  queryContent('blog').sort({ week: -1 }).find()
)

const filteredPosts = computed(() => {
  let list = posts.value ?? []
  if (search.value.trim()) {
    const q = search.value.toLowerCase()
    list = list.filter(
      p =>
        p.title?.toLowerCase().includes(q) ||
        p.description?.toLowerCase().includes(q) ||
        p.tags?.some((t: string) => t.toLowerCase().includes(q))
    )
  }
  if (sortOrder.value === 'oldest') {
    return [...list].sort((a, b) => (a.week ?? 0) - (b.week ?? 0))
  }
  return list
})
</script>

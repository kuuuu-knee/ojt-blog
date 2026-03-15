<template>
  <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
    <!-- Page header -->
    <div class="mb-10">
      <h1 class="text-3xl font-extrabold text-gray-900 mb-2">Weekly OJT Posts</h1>
      <p class="text-gray-500">A chronological journal of my internship experience, week by week.</p>
    </div>

    <!-- Timeline list -->
    <div v-if="posts && posts.length" class="relative">
      <!-- Vertical line -->
      <div class="absolute left-5 top-0 bottom-0 w-0.5 bg-primary-100 hidden sm:block" aria-hidden="true" />

      <div class="space-y-6">
        <div
          v-for="post in posts"
          :key="post._path"
          class="relative sm:pl-16"
        >
          <!-- Timeline dot -->
          <div class="hidden sm:flex absolute left-0 w-10 h-10 rounded-full bg-primary-600 text-white items-center justify-center text-xs font-bold shadow-md">
            W{{ post.week }}
          </div>

          <!-- Post card -->
          <NuxtLink
            :to="`/blog/${post._path.split('/').pop()}`"
            class="card group flex flex-col sm:flex-row gap-4 p-5"
          >
            <!-- Cover thumbnail -->
            <div v-if="post.coverImage" class="sm:w-40 sm:h-28 rounded-lg overflow-hidden flex-shrink-0 bg-gray-100">
              <img
                :src="post.coverImage"
                :alt="post.title"
                class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300"
                loading="lazy"
              />
            </div>
            <div v-else class="sm:w-40 sm:h-28 rounded-lg flex-shrink-0 bg-gradient-to-br from-primary-100 to-primary-200 flex items-center justify-center">
              <span class="text-3xl">📓</span>
            </div>

            <!-- Content -->
            <div class="flex-1 min-w-0">
              <div class="flex flex-wrap items-center gap-2 mb-2">
                <span class="badge-week sm:hidden">Week {{ post.week }}</span>
                <time class="text-xs text-gray-400">{{ formatDate(post.date) }}</time>
              </div>
              <h2 class="font-bold text-gray-900 text-lg leading-snug mb-1 group-hover:text-primary-600 transition-colors line-clamp-2">
                {{ post.title }}
              </h2>
              <p v-if="post.description" class="text-sm text-gray-500 line-clamp-2">
                {{ post.description }}
              </p>
              <div class="mt-3 flex items-center gap-1 text-xs font-medium text-primary-600">
                Read more
                <svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                </svg>
              </div>
            </div>
          </NuxtLink>
        </div>
      </div>
    </div>

    <!-- Empty state -->
    <div v-else class="text-center py-20 text-gray-400">
      <span class="text-5xl block mb-4">📭</span>
      <p class="text-lg font-medium">No posts yet</p>
      <p class="text-sm mt-1">Check back next week for the first entry!</p>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'Weekly Posts — OJT Blog' })

const { data: posts } = await useAsyncData('all-posts', () =>
  queryContent('posts').sort({ week: -1 }).find()
)

function formatDate(dateStr) {
  if (!dateStr) return ''
  return new Date(dateStr).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  })
}
</script>

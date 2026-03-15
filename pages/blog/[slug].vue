<template>
  <div>
    <div v-if="post" class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
      <!-- Back link -->
      <NuxtLink to="/blog" class="inline-flex items-center gap-1.5 text-sm text-gray-500 hover:text-primary-600 mb-8 transition-colors">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
        </svg>
        Back to all posts
      </NuxtLink>

      <!-- Post header -->
      <header class="mb-8">
        <div class="flex flex-wrap items-center gap-3 mb-4">
          <span class="badge-week">Week {{ post.week }}</span>
          <time class="text-sm text-gray-400 font-medium">{{ formatDate(post.date) }}</time>
        </div>
        <h1 class="text-3xl sm:text-4xl font-extrabold text-gray-900 leading-tight mb-4">
          {{ post.title }}
        </h1>
        <p v-if="post.description" class="text-lg text-gray-500 leading-relaxed">
          {{ post.description }}
        </p>
      </header>

      <!-- Cover image -->
      <div v-if="post.coverImage" class="mb-8 rounded-2xl overflow-hidden shadow-md aspect-video bg-gray-100">
        <img
          :src="post.coverImage"
          :alt="post.title"
          class="w-full h-full object-cover"
        />
      </div>

      <!-- Post content -->
      <article class="prose-content mb-10">
        <ContentRenderer :value="post" />
      </article>

      <!-- Image gallery -->
      <ImageGallery v-if="post.images && post.images.length" :images="post.images" />

      <!-- Post meta footer -->
      <div class="border-t border-gray-100 pt-6 mt-10 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
        <div class="text-sm text-gray-400">
          Posted on <time>{{ formatDate(post.date) }}</time>
        </div>
        <NuxtLink to="/blog" class="text-sm font-medium text-primary-600 hover:text-primary-800 flex items-center gap-1">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
          All posts
        </NuxtLink>
      </div>
    </div>

    <!-- 404 fallback -->
    <div v-else class="max-w-3xl mx-auto px-4 py-20 text-center text-gray-400">
      <span class="text-5xl block mb-4">😕</span>
      <p class="text-lg font-medium">Post not found</p>
      <NuxtLink to="/blog" class="btn-primary mt-6">Back to blog</NuxtLink>
    </div>
  </div>
</template>

<script setup>
const route = useRoute()
const slug = route.params.slug

const { data: post } = await useAsyncData(`post-${slug}`, () =>
  queryContent('posts', slug).findOne()
)

if (post.value) {
  useHead({
    title: `Week ${post.value.week}: ${post.value.title} — OJT Blog`,
    meta: [
      { name: 'description', content: post.value.description },
    ],
  })
}

function formatDate(dateStr) {
  if (!dateStr) return ''
  return new Date(dateStr).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  })
}
</script>

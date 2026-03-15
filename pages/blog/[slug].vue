<template>
  <div>
    <div v-if="pending" class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 py-16 animate-pulse">
      <div class="h-4 bg-gray-200 rounded w-24 mb-4" />
      <div class="h-10 bg-gray-200 rounded w-3/4 mb-4" />
      <div class="h-4 bg-gray-200 rounded w-1/3 mb-10" />
      <div class="space-y-3">
        <div v-for="i in 8" :key="i" class="h-4 bg-gray-200 rounded" />
      </div>
    </div>

    <template v-else-if="post">
      <!-- Post Header -->
      <div class="bg-gradient-to-br from-brand-800 to-brand-600 text-white py-16">
        <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
          <div class="flex items-center gap-2 mb-5">
            <NuxtLink to="/blog" class="text-sm text-blue-200 hover:text-white transition-colors">
              ← Back to Blog
            </NuxtLink>
          </div>
          <div class="flex flex-wrap gap-2 mb-4">
            <span class="badge bg-white/20 text-white">Week {{ post.week }}</span>
            <span v-for="tag in post.tags" :key="tag" class="badge bg-white/10 text-blue-100">
              {{ tag }}
            </span>
          </div>
          <h1 class="text-3xl sm:text-4xl font-bold font-serif leading-tight mb-4">
            {{ post.title }}
          </h1>
          <div class="flex items-center gap-4 text-sm text-blue-200">
            <span>📅 {{ post.date }}</span>
            <span v-if="post.readTime">🕐 {{ post.readTime }} min read</span>
          </div>
        </div>
      </div>

      <!-- Cover Image -->
      <div v-if="post.coverImage" class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 -mt-6">
        <div class="rounded-xl overflow-hidden shadow-lg aspect-video bg-gray-100">
          <img
            :src="post.coverImage"
            :alt="post.title"
            class="w-full h-full object-cover"
            loading="lazy"
          >
        </div>
      </div>

      <!-- Summary Card -->
      <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 mt-8">
        <div class="card p-6 grid sm:grid-cols-3 gap-4 bg-brand-50 border-brand-100">
          <div>
            <p class="text-xs font-semibold uppercase tracking-wide text-brand-600 mb-1">Week</p>
            <p class="font-medium text-gray-800">Week {{ post.week }}</p>
          </div>
          <div>
            <p class="text-xs font-semibold uppercase tracking-wide text-brand-600 mb-1">Date</p>
            <p class="font-medium text-gray-800">{{ post.date }}</p>
          </div>
          <div>
            <p class="text-xs font-semibold uppercase tracking-wide text-brand-600 mb-1">Focus</p>
            <p class="font-medium text-gray-800">{{ post.focus ?? 'General Tasks' }}</p>
          </div>
        </div>
      </div>

      <!-- Post Content -->
      <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 py-10">
        <article class="prose prose-lg prose-blue max-w-none
                        prose-headings:font-serif prose-headings:text-gray-900
                        prose-a:text-brand-600 prose-a:no-underline hover:prose-a:underline
                        prose-img:rounded-xl prose-img:shadow-md prose-img:mx-auto
                        prose-blockquote:border-brand-400 prose-blockquote:bg-brand-50 prose-blockquote:py-1 prose-blockquote:px-4 prose-blockquote:rounded-r-lg">
          <ContentRenderer :value="post" />
        </article>
      </div>

      <!-- Image Gallery -->
      <div v-if="post.images && post.images.length" class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 pb-10">
        <h2 class="text-xl font-bold text-gray-900 mb-5">📷 Photo Gallery</h2>
        <div class="grid grid-cols-2 sm:grid-cols-3 gap-3">
          <button
            v-for="(img, idx) in post.images"
            :key="idx"
            class="group relative aspect-square rounded-xl overflow-hidden bg-gray-100 shadow-sm hover:shadow-md transition-shadow"
            @click="openLightbox(idx)"
          >
            <img
              :src="img.src"
              :alt="img.alt ?? `Image ${idx + 1}`"
              class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300"
              loading="lazy"
            >
            <div class="absolute inset-0 bg-black/0 group-hover:bg-black/10 transition-colors" />
          </button>
        </div>
      </div>

      <!-- Post Navigation -->
      <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 pb-16">
        <div class="flex flex-col sm:flex-row gap-4">
          <NuxtLink
            v-if="prevPost"
            :to="prevPost._path"
            class="card flex-1 p-4 group hover:border-brand-200"
          >
            <p class="text-xs text-gray-400 mb-1">← Previous</p>
            <p class="font-medium text-gray-700 group-hover:text-brand-600 transition-colors line-clamp-1">
              {{ prevPost.title }}
            </p>
          </NuxtLink>
          <NuxtLink
            v-if="nextPost"
            :to="nextPost._path"
            class="card flex-1 p-4 text-right group hover:border-brand-200"
          >
            <p class="text-xs text-gray-400 mb-1">Next →</p>
            <p class="font-medium text-gray-700 group-hover:text-brand-600 transition-colors line-clamp-1">
              {{ nextPost.title }}
            </p>
          </NuxtLink>
        </div>
      </div>
    </template>

    <!-- 404 State -->
    <div v-else class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 py-24 text-center">
      <p class="text-5xl mb-4">😕</p>
      <h2 class="text-2xl font-bold text-gray-800 mb-2">Post Not Found</h2>
      <p class="text-gray-500 mb-6">The post you're looking for doesn't exist.</p>
      <NuxtLink to="/blog" class="btn-primary">← Back to Blog</NuxtLink>
    </div>

    <!-- Lightbox -->
    <Teleport to="body">
      <div
        v-if="lightboxOpen"
        class="fixed inset-0 bg-black/90 z-50 flex items-center justify-center p-4"
        @click.self="closeLightbox"
      >
        <button
          class="absolute top-4 right-4 text-white/70 hover:text-white p-2"
          aria-label="Close"
          @click="closeLightbox"
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
        <button
          v-if="lightboxIndex > 0"
          class="absolute left-4 text-white/70 hover:text-white p-2"
          aria-label="Previous"
          @click="lightboxIndex--"
        >
          <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
        </button>
        <img
          v-if="post?.images"
          :src="post.images[lightboxIndex]?.src"
          :alt="post.images[lightboxIndex]?.alt ?? ''"
          class="max-h-[85vh] max-w-full rounded-lg shadow-2xl object-contain"
        >
        <button
          v-if="post?.images && lightboxIndex < post.images.length - 1"
          class="absolute right-4 text-white/70 hover:text-white p-2"
          aria-label="Next"
          @click="lightboxIndex++"
        >
          <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </button>
      </div>
    </Teleport>
  </div>
</template>

<script setup lang="ts">
const route = useRoute()

const { data: post, pending } = await useAsyncData(`post-${route.params.slug}`, () =>
  queryContent('blog', route.params.slug as string).findOne()
)

if (!post.value) {
  throw createError({ statusCode: 404, statusMessage: 'Post not found' })
}

useHead({
  title: computed(() => `${post.value?.title ?? 'Post'} — OJT Blog`),
  meta: [
    { name: 'description', content: computed(() => post.value?.description ?? '') },
  ],
})

// Sibling navigation
const { data: siblings } = await useAsyncData(`siblings-${route.params.slug}`, () =>
  queryContent('blog').sort({ week: 1 }).only(['_path', 'title', 'week']).find()
)

const currentIndex = computed(() =>
  siblings.value?.findIndex(p => p._path === post.value?._path) ?? -1
)
const prevPost = computed(() =>
  currentIndex.value > 0 ? siblings.value?.[currentIndex.value - 1] : null
)
const nextPost = computed(() =>
  currentIndex.value !== -1 && currentIndex.value < (siblings.value?.length ?? 0) - 1
    ? siblings.value?.[currentIndex.value + 1]
    : null
)

// Lightbox
const lightboxOpen = ref(false)
const lightboxIndex = ref(0)

function openLightbox(idx: number) {
  lightboxIndex.value = idx
  lightboxOpen.value = true
}
function closeLightbox() {
  lightboxOpen.value = false
}

// Close lightbox on Escape
onMounted(() => {
  const handler = (e: KeyboardEvent) => {
    if (e.key === 'Escape') closeLightbox()
    if (e.key === 'ArrowLeft' && lightboxIndex.value > 0) lightboxIndex.value--
    if (e.key === 'ArrowRight' && post.value?.images && lightboxIndex.value < post.value.images.length - 1)
      lightboxIndex.value++
  }
  document.addEventListener('keydown', handler)
  onUnmounted(() => document.removeEventListener('keydown', handler))
})
</script>

<template>
  <div>
    <!-- Hero Section -->
    <section class="bg-gradient-to-br from-brand-700 via-brand-600 to-brand-500 text-white">
      <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-20 sm:py-28">
        <div class="max-w-2xl">
          <span class="badge bg-white/20 text-white mb-4">📚 On-the-Job Training Journal</span>
          <h1 class="text-4xl sm:text-5xl font-bold font-serif leading-tight mb-5">
            My OJT Journey
          </h1>
          <p class="text-lg sm:text-xl text-blue-100 leading-relaxed mb-8">
            Welcome! I'm documenting my On-the-Job Training experience week by week — the tasks I tackle,
            challenges I overcome, and the lessons I carry forward.
          </p>
          <div class="flex flex-wrap gap-3">
            <NuxtLink to="/blog" class="btn-primary bg-white text-brand-700 hover:bg-blue-50">
              📖 Read the Blog
            </NuxtLink>
            <NuxtLink to="/about" class="btn-outline border-white/60 text-white hover:bg-white/10">
              👋 About Me
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Strip -->
    <section class="bg-white border-b border-gray-100">
      <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
        <div class="grid grid-cols-2 sm:grid-cols-4 gap-6">
          <div v-for="stat in stats" :key="stat.label" class="text-center">
            <div class="text-3xl font-bold text-brand-600">{{ stat.value }}</div>
            <div class="text-sm text-gray-500 mt-1">{{ stat.label }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Latest Posts -->
    <section class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-14">
      <div class="flex items-center justify-between mb-8">
        <div>
          <h2 class="text-2xl font-bold text-gray-900">Latest Weekly Updates</h2>
          <p class="text-gray-500 mt-1">My most recent OJT reflections</p>
        </div>
        <NuxtLink to="/blog" class="btn-outline hidden sm:inline-flex">
          View All →
        </NuxtLink>
      </div>

      <div v-if="pending" class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <div v-for="i in 3" :key="i" class="card p-6 animate-pulse">
          <div class="h-4 bg-gray-200 rounded w-1/4 mb-3" />
          <div class="h-6 bg-gray-200 rounded w-3/4 mb-2" />
          <div class="h-4 bg-gray-200 rounded w-full mb-1" />
          <div class="h-4 bg-gray-200 rounded w-5/6" />
        </div>
      </div>

      <div v-else class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <PostCard
          v-for="post in latestPosts"
          :key="post._path"
          :post="post"
        />
      </div>

      <div class="mt-8 text-center sm:hidden">
        <NuxtLink to="/blog" class="btn-outline">View All Posts →</NuxtLink>
      </div>
    </section>

    <!-- Timeline Preview -->
    <section class="bg-white border-t border-gray-100 py-14">
      <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
        <h2 class="text-2xl font-bold text-gray-900 mb-2">OJT Timeline</h2>
        <p class="text-gray-500 mb-10">A quick look at my internship week by week</p>

        <div v-if="!pending" class="relative">
          <!-- Vertical line -->
          <div class="absolute left-4 top-0 bottom-0 w-0.5 bg-brand-100 hidden sm:block" />

          <div class="space-y-6">
            <div
              v-for="post in allPosts"
              :key="post._path"
              class="sm:pl-12 relative"
            >
              <!-- Dot -->
              <div class="hidden sm:flex absolute left-0 top-1 w-8 h-8 rounded-full bg-brand-100 border-2 border-brand-400 items-center justify-center">
                <span class="text-xs font-bold text-brand-700">{{ post.week }}</span>
              </div>

              <NuxtLink :to="post._path" class="group flex items-start gap-4">
                <div class="sm:hidden w-8 h-8 rounded-full bg-brand-100 border-2 border-brand-400 flex items-center justify-center flex-shrink-0">
                  <span class="text-xs font-bold text-brand-700">{{ post.week }}</span>
                </div>
                <div>
                  <p class="text-xs text-gray-400 mb-0.5">{{ post.date }}</p>
                  <h3 class="font-semibold text-gray-800 group-hover:text-brand-600 transition-colors">
                    {{ post.title }}
                  </h3>
                  <p class="text-sm text-gray-500 mt-0.5 line-clamp-1">{{ post.description }}</p>
                </div>
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
const { data: allPosts, pending } = await useAsyncData('home-posts', () =>
  queryContent('blog').sort({ week: -1 }).find()
)

const latestPosts = computed(() => (allPosts.value ?? []).slice(0, 3))

const stats = computed(() => [
  { value: allPosts.value?.length ?? 0, label: 'Weekly Posts' },
  { value: '128', label: 'Hours Logged' },
  { value: '1', label: 'Company' },
])
</script>

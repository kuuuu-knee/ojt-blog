<template>
  <div v-if="images && images.length" class="my-8">
    <h3 class="text-lg font-semibold text-gray-800 mb-4 flex items-center gap-2">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-primary-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
      </svg>
      Photo Gallery
    </h3>
    <div class="grid grid-cols-2 sm:grid-cols-3 gap-3">
      <button
        v-for="(img, i) in images"
        :key="i"
        class="aspect-square rounded-xl overflow-hidden bg-gray-100 focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2"
        @click="openLightbox(i)"
      >
        <img
          :src="img.src"
          :alt="img.alt || `Photo ${i + 1}`"
          class="w-full h-full object-cover hover:scale-105 transition-transform duration-300"
          loading="lazy"
        />
      </button>
    </div>

    <!-- Lightbox -->
    <Teleport to="body">
      <Transition name="fade">
        <div
          v-if="lightboxIndex !== null"
          class="fixed inset-0 z-50 bg-black/80 flex items-center justify-center p-4"
          @click.self="closeLightbox"
        >
          <div class="relative max-w-4xl w-full">
            <img
              :src="images[lightboxIndex].src"
              :alt="images[lightboxIndex].alt || `Photo ${lightboxIndex + 1}`"
              class="w-full max-h-[80vh] object-contain rounded-xl"
            />
            <p v-if="images[lightboxIndex].caption" class="text-center text-white/80 text-sm mt-3">
              {{ images[lightboxIndex].caption }}
            </p>

            <!-- Close -->
            <button
              class="absolute top-3 right-3 p-2 rounded-full bg-black/40 text-white hover:bg-black/60 transition-colors"
              aria-label="Close lightbox"
              @click="closeLightbox"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>

            <!-- Prev -->
            <button
              v-if="lightboxIndex > 0"
              class="absolute left-3 top-1/2 -translate-y-1/2 p-2 rounded-full bg-black/40 text-white hover:bg-black/60 transition-colors"
              aria-label="Previous image"
              @click="lightboxIndex--"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
              </svg>
            </button>

            <!-- Next -->
            <button
              v-if="lightboxIndex < images.length - 1"
              class="absolute right-3 top-1/2 -translate-y-1/2 p-2 rounded-full bg-black/40 text-white hover:bg-black/60 transition-colors"
              aria-label="Next image"
              @click="lightboxIndex++"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </button>

            <!-- Counter -->
            <p class="absolute bottom-3 left-1/2 -translate-x-1/2 text-white/70 text-xs font-medium bg-black/40 px-3 py-1 rounded-full">
              {{ lightboxIndex + 1 }} / {{ images.length }}
            </p>
          </div>
        </div>
      </Transition>
    </Teleport>
  </div>
</template>

<script setup>
const props = defineProps({
  images: {
    type: Array,
    default: () => [],
  },
})

const lightboxIndex = ref(null)

function openLightbox(index) {
  lightboxIndex.value = index
}

function closeLightbox() {
  lightboxIndex.value = null
}

onMounted(() => {
  const onKey = (e) => {
    if (lightboxIndex.value === null) return
    if (e.key === 'Escape') closeLightbox()
    if (e.key === 'ArrowLeft' && lightboxIndex.value > 0) lightboxIndex.value--
    if (e.key === 'ArrowRight' && lightboxIndex.value < props.images.length - 1) lightboxIndex.value++
  }
  window.addEventListener('keydown', onKey)
  onUnmounted(() => window.removeEventListener('keydown', onKey))
})
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

<template>
  <footer class="bg-white border-t border-gray-100 mt-16">
    <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <div class="flex flex-col sm:flex-row items-center justify-between gap-4">
        <div class="flex items-center gap-2 text-gray-600">
          <span class="text-xl">📝</span>
          <span class="font-semibold text-gray-800">OJT Blog</span>
          <span class="text-sm text-gray-500">— My Internship Journey</span>
        </div>
        <p class="text-sm text-gray-400">
          &copy; {{ new Date().getFullYear() }} · Built with
          <a
            href="https://nuxt.com"
            target="_blank"
            rel="noopener noreferrer"
            class="text-primary-500 hover:text-primary-700 transition-colors"
          >Nuxt 3</a>
          &amp;
          <a
            href="https://tailwindcss.com"
            target="_blank"
            rel="noopener noreferrer"
            class="text-primary-500 hover:text-primary-700 transition-colors"
          >Tailwind CSS</a>
        </p>
      </div>
    </div>
  </footer>
</template>

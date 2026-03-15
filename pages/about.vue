<template>
  <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
    <h1 class="text-3xl font-extrabold text-gray-900 mb-6">About Me</h1>

    <div class="card p-6 sm:p-8 mb-8">
      <div class="flex flex-col sm:flex-row items-start gap-6">
        <!-- Avatar placeholder -->
        <div class="w-24 h-24 rounded-full bg-gradient-to-br from-primary-400 to-primary-600 flex items-center justify-center flex-shrink-0 text-white text-4xl font-bold">
          👤
        </div>
        <div>
          <h2 class="text-xl font-bold text-gray-900 mb-1">OJT Intern</h2>
          <p class="text-primary-600 font-medium text-sm mb-4">On-the-Job Trainee</p>
          <p class="text-gray-600 leading-relaxed">
            Hi! I'm an intern currently undergoing On-the-Job Training (OJT). This blog is my
            digital journal where I document my weekly experiences, tasks, challenges, and growth
            during my internship.
          </p>
        </div>
      </div>
    </div>

    <div class="prose-content">
      <h2>What is this blog?</h2>
      <p>
        This is a personal blog that serves as a portfolio and journal of my OJT journey.
        Each week I post an update covering:
      </p>
      <ul>
        <li>Tasks and projects I worked on</li>
        <li>Challenges I encountered and how I solved them</li>
        <li>Key lessons and skills I learned</li>
        <li>Photos from the workplace or projects</li>
      </ul>

      <h2>About the OJT Program</h2>
      <p>
        On-the-Job Training (OJT) is a practical component of my academic program that gives
        me hands-on experience in a real-world professional environment. It helps bridge the gap
        between classroom learning and industry practice.
      </p>

      <h2>Tech Stack for This Blog</h2>
      <ul>
        <li><strong>Nuxt 3</strong> — Vue 3 framework for the frontend</li>
        <li><strong>Tailwind CSS</strong> — Utility-first styling</li>
        <li><strong>@nuxt/content</strong> — Markdown-based blog posts</li>
        <li><strong>GitHub Pages / VPS</strong> — Deployment</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'About — OJT Blog' })
</script>

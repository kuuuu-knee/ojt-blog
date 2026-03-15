<template>
  <div>
    <div class="bg-gradient-to-r from-brand-700 to-brand-500 text-white py-14">
      <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
        <span class="badge bg-white/20 text-white mb-3">👋 About Me</span>
        <h1 class="text-3xl sm:text-4xl font-bold font-serif mb-3">About This Blog</h1>
        <p class="text-blue-100 max-w-xl">
          A little about me, my internship, and why I'm documenting this journey.
        </p>
      </div>
    </div>

    <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
      <div class="card p-8 sm:p-10">
        <div class="flex flex-col sm:flex-row gap-8 items-start">
          <!-- Avatar Placeholder -->
          <div class="w-28 h-28 rounded-2xl bg-gradient-to-br from-brand-400 to-brand-600 flex items-center justify-center text-5xl flex-shrink-0 shadow-md">
            🎓
          </div>

          <div>
            <h2 class="text-2xl font-bold text-gray-900 mb-1">OJT Student</h2>
            <p class="text-brand-600 font-medium mb-4">IT Intern · Information Technology Student</p>
            <p class="text-gray-600 leading-relaxed">
              Hi! I'm currently on my On-the-Job Training (OJT) as part of my degree program in
              Information Technology. This blog documents my internship journey — from the first day jitters
              to growing into a contributing team member.
            </p>
          </div>
        </div>

        <hr class="my-8 border-gray-100">

        <div class="grid sm:grid-cols-2 gap-8">
          <div>
            <h3 class="font-semibold text-gray-900 mb-3 flex items-center gap-2">
              🏢 Internship Details
            </h3>
            <ul class="space-y-2 text-sm text-gray-600">
              <li class="flex items-start gap-2">
                <span class="text-brand-500 mt-0.5">•</span>
                <span><strong>Role:</strong> Software Development Intern</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="text-brand-500 mt-0.5">•</span>
                <span><strong>Duration:</strong> 486 hours (approx. 12 weeks)</span>
              </li>
              <li class="flex items-start gap-2">
                <span class="text-brand-500 mt-0.5">•</span>
                <span><strong>Department:</strong> IT</span>
              </li>
            </ul>
          </div>

          <div>
            <h3 class="font-semibold text-gray-900 mb-3 flex items-center gap-2">
              🛠️ Tech Stack I'm Learning
            </h3>
            <div class="flex flex-wrap gap-2">
              <span v-for="tech in techStack" :key="tech" class="badge bg-brand-50 text-brand-700">
                {{ tech }}
              </span>
            </div>
          </div>
        </div>

        <hr class="my-8 border-gray-100">

        <div>
          <h3 class="font-semibold text-gray-900 mb-3">🎯 Goals for this OJT</h3>
          <ul class="space-y-2">
            <li
              v-for="goal in goals"
              :key="goal"
              class="flex items-start gap-3 text-sm text-gray-600"
            >
              <span class="text-brand-500 mt-0.5">✓</span>
              <span>{{ goal }}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
useHead({ title: 'About — OJT Blog' })

const techStack = [
  'Nuxt 3', 'Tailwind CSS',
  'Git', 'Laravel API', 'Node.js', 'MariaDB',
]

const goals = [
  'Apply classroom knowledge to real-world software development',
  'Collaborate effectively with a professional development team',
  'Improve problem-solving skills under realistic project constraints',
  'Learn industry best practices for code quality and project management',
  'Build a portfolio of work samples to showcase to future employers',
]
</script>

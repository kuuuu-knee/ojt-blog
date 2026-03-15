---
week: 2
title: "Deep Dive — Building My First Feature"
date: "2025-01-13"
description: "This week I was assigned my first real feature to implement: a user profile page. I worked with Vue 3 components, Tailwind CSS, and an existing REST API."
coverImage: "/images/week2-cover.jpg"
images:
  - src: "/images/week2-figma.jpg"
    alt: "Figma design mockup for the user profile page"
    caption: "Figma design I worked from"
  - src: "/images/week2-code.jpg"
    alt: "VS Code with the component I built"
    caption: "Writing the ProfileCard component"
  - src: "/images/week2-preview.jpg"
    alt: "Browser preview of the finished profile page"
    caption: "Final result in the browser"
---

## Overview

Week 2 was where things started feeling real. I was assigned my first actual feature: building a **user profile page** from a Figma design. This involved creating Vue components, making API calls, and applying Tailwind CSS classes to match the design closely.

## Tasks Performed

- **Read the Figma design** — Reviewed the UI mockup provided by the design team and clarified spacing and color values.
- **Created `ProfileCard.vue`** — Built a reusable component showing the user's avatar, name, role, and bio.
- **API Integration** — Used `useFetch()` in Nuxt to pull user data from the REST API endpoint `/api/users/:id`.
- **Responsive Layout** — Made the profile page work on mobile, tablet, and desktop using Tailwind's responsive prefixes (`sm:`, `md:`, `lg:`).
- **Code Review** — Submitted a pull request and incorporated feedback from my supervisor.

## Challenges Encountered

The biggest challenge was matching the Figma design pixel-perfectly. I spent extra time on:

- Getting the avatar image to display as a perfect circle with a border
- Aligning the bio text and action buttons correctly on smaller screens

## Lessons Learned

1. **Tailwind responsive utilities** are incredibly powerful once you learn the breakpoint system.
2. **`useFetch` vs `useAsyncData`** — understanding when to use each Nuxt composable for data fetching.
3. **Breaking UI into small components** — it's easier to reason about a `ProfileCard`, `ProfileStats`, and `ProfileActions` separately than one giant component.

## Code Snippet

```vue
<template>
  <div class="flex flex-col items-center p-6 bg-white rounded-xl shadow-sm">
    <img :src="user.avatar" :alt="user.name" class="w-20 h-20 rounded-full border-4 border-primary-200" />
    <h2 class="mt-4 text-xl font-bold text-gray-900">{{ user.name }}</h2>
    <p class="text-sm text-gray-500">{{ user.role }}</p>
  </div>
</template>
```

## Reflection

Getting real design-to-code experience this week was incredibly valuable. The PR review process taught me that clean, readable code matters as much as code that works. I'll be more deliberate about naming and structure going forward.

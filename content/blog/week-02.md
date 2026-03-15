---
title: "First Bug Fix and Code Review Survival Guide"
week: 2
date: "January 13, 2025"
description: "Tackling my first real bug, surviving a code review, and learning that reading other people's code is a skill of its own."
focus: "Bug Fixing & Code Review"
readTime: 5
tags:
  - debugging
  - code-review
  - vue
coverImage: /images/week2-cover.jpg
images:
  - src: /images/week2-bugfix.jpg
    alt: Debugging session on the admin dashboard
  - src: /images/week2-review.jpg
    alt: Code review on GitHub
---

## 🐛 My First Bug Ticket

Monday morning, a Jira ticket landed in my queue:

> **BUG-142:** *Admin dashboard table does not render when the API returns an empty array.*

Sir Mark assigned it to me with a note: *"Good starter task. Shouldn't take more than a day."*

It took me two.

## 🔍 Digging Into the Codebase

The admin dashboard is a Vue 3 component about 400 lines long. I spent the first few hours just reading — trying to understand the data flow before touching anything. The bug was in a `v-if` condition that didn't account for the empty array case:

```vue
<!-- Before (broken) -->
<template v-if="data">
  <DataTable :rows="data" />
</template>

<!-- After (fixed) -->
<template v-if="data && data.length > 0">
  <DataTable :rows="data" />
</template>
<template v-else>
  <EmptyState message="No records found." />
</template>
```

Simple fix. Long journey to get there.

## 👀 Surviving the Code Review

I opened a pull request on GitHub and Sir Mark reviewed it within the hour. His feedback:

- ✅ Correct fix
- 🔄 Rename `data` to something more descriptive (`tableRows`)
- 📝 Add a comment explaining *why* the empty check is needed
- 🧪 Write a unit test for the empty state

I hadn't thought about the test. Back to work.

## 📋 Tasks This Week

1. Fix BUG-142 on the admin dashboard
2. Write a unit test for the fix using Vitest
3. Attend daily standups (15-minute morning check-ins)
4. Study the codebase's component library and design system

## 😓 Challenges

Writing the unit test was harder than fixing the bug. The project uses Vitest + Vue Test Utils, neither of which I had used before. I spent an afternoon reading documentation and adapting an existing test as a template.

Also: **code reviews feel very personal at first.** Every comment felt like a critique of me, not just the code. I had to remind myself that feedback is how teams maintain quality — it's not personal.

## 💡 Lessons Learned

> **"Others' code is written in a foreign language that you learn to read before you write."**

- Always run the existing tests before making changes (some were already failing — not my fault!)
- Empty/null states are *first-class* UI concerns, not afterthoughts
- `v-if` vs `v-show` matters for performance — I asked and got a 20-minute lesson from the senior dev

## 🔜 Next Week

I'll be assigned a slightly larger feature: adding a date-range filter to the dashboard table. My first feature from scratch. The nervous butterflies are back!

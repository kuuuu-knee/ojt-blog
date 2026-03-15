---
title: "Building My First Feature: Date Range Filter"
week: 3
date: "January 20, 2025"
description: "From requirements to deployed feature — building a date-range filter for the admin dashboard and learning about component design along the way."
focus: "Feature Development"
readTime: 6
tags:
  - feature
  - components
  - vue
  - api
coverImage: /images/week3-cover.jpg
images:
  - src: /images/week3-filter-ui.jpg
    alt: The date-range filter component
  - src: /images/week3-pr.jpg
    alt: Pull request merged
  - src: /images/week3-standup.jpg
    alt: Daily standup notes
---

## 🚀 My First Real Feature

This week I went from "bug fixer" to "feature developer" — at least in my own head. The task:

> **FEAT-78:** *Add a start-date / end-date filter to the admin transactions table.*

The acceptance criteria were clear: two date inputs, a "Filter" button, API call with query params, and the table should refresh. Sounds simple. Almost always is, until you start.

## 🎨 Component Design

I started by breaking the feature into smaller pieces:

1. A `DateRangeFilter.vue` component with two `<input type="date">` fields
2. An event emitted to the parent when the user clicks "Filter"
3. The parent passes the dates as query parameters to the API composable

Here's the core of the filter component:

```vue
<script setup lang="ts">
const emit = defineEmits<{
  filter: [{ from: string; to: string }]
}>()

const from = ref('')
const to = ref('')

function applyFilter() {
  if (!from.value || !to.value) return
  emit('filter', { from: from.value, to: to.value })
}
</script>
```

The senior dev suggested using `defineEmits` with typed generics — a pattern I hadn't seen before. The code is much more self-documenting this way.

## 🌐 Working with the API

The backend API accepts optional `startDate` and `endDate` query parameters:

```
GET /api/transactions?startDate=2025-01-01&endDate=2025-01-31
```

I updated the `useTransactions` composable to accept these as optional arguments and pass them to the Axios request. I learned about `URLSearchParams` as a clean way to build query strings.

## 📋 Tasks This Week

1. Build `DateRangeFilter.vue` component
2. Integrate filter with the transactions API composable
3. Handle loading and error states during filtered fetch
4. Write component tests for the date validation logic
5. Get the PR reviewed and merged by end of Friday

## ✅ PR Merged — But Not Without Feedback

Sir Mark approved the PR after two rounds of review. Feedback highlights:

- Validate that `from` date is not after `to` date (I missed this!)
- Disable the "Filter" button while a request is in-flight (UX improvement)
- Clear filter results if either date input is cleared

I addressed all three. The validation feedback especially stung a bit — it was a logical edge case I should have caught during testing.

## 😓 Challenges

The hardest part wasn't the code; it was **understanding the existing API contract**. The backend documentation was outdated and said the parameter was `start_date` (snake_case) but the actual API expected `startDate` (camelCase). I spent two hours debugging a silent 200-OK response with empty data before finding this.

**Lesson:** Never trust outdated docs. Test the API directly with Postman first.

## 💡 Lessons Learned

> **Build for the unhappy path first.** Validating bad input, handling loading states, and showing empty states make the difference between intern-level and professional-level code.

- `defineEmits` with TypeScript generics makes component contracts explicit
- Date inputs are tricky across browsers — always test in Chrome *and* Firefox
- Postman is your best friend when the documentation lies

## 📸 Team Moment

On Friday, Carla (the other intern) and I were both presenting our work to the team in the weekly demo meeting. It was nerve-wracking presenting to eight people, but seeing my feature in action on the screen felt incredibly rewarding. Carla crushed her presentation too.

## 🔜 Next Week

I'll start learning about the database layer — writing my first SQL queries through the ORM. Sir Mark says "you'll understand why the API feels the way it does once you see the schema." Looking forward to the deep dive.

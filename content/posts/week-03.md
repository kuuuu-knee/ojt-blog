---
week: 3
title: "Bug Hunt & Teamwork — Debugging and Collaboration"
date: "2025-01-20"
description: "Week 3 was all about debugging a tricky production bug, attending my first sprint planning meeting, and learning how to collaborate effectively on a team project."
coverImage: "/images/week3-cover.jpg"
images:
  - src: "/images/week3-standup.jpg"
    alt: "Daily standup meeting with the team"
    caption: "My first sprint planning session"
  - src: "/images/week3-debug.jpg"
    alt: "Debugging session in the browser DevTools"
    caption: "Tracking down that elusive bug in DevTools"
---

## Overview

My third week introduced me to two important aspects of professional development: **debugging production issues** and **agile team collaboration**. Both were eye-opening experiences that no classroom can fully prepare you for.

## Tasks Performed

- **Sprint Planning** — Participated in the team's two-week sprint planning meeting. I helped estimate story points for tasks I could own.
- **Bug Investigation** — Investigated a reported bug where the search filter was returning incorrect results on page 2+ of paginated data.
- **Root Cause Analysis** — Traced the bug to an off-by-one error in the offset calculation for the API query.
- **Bug Fix & Tests** — Fixed the offset calculation and added a test case to prevent regression.
- **Documentation** — Updated the internal wiki page describing the pagination utility function.

## The Bug

The search feature passed the wrong `offset` value when navigating beyond page 1:

```js
// ❌ Before (off by one)
const offset = page * pageSize

// ✅ After (correct)
const offset = (page - 1) * pageSize
```

This caused the API to skip one item per page, resulting in missed search results.

## Challenges Encountered

Finding the bug took longer than expected because the issue only appeared when combining search filters *with* pagination — it didn't reproduce with one or the other alone. Learning to **isolate variables** when debugging was key.

## Lessons Learned

1. **Regression tests matter** — The bug existed for weeks because there was no test covering the combination of search + pagination.
2. **Read the issue report carefully** — The initial report mentioned "page 2" specifically; I should have started testing there immediately.
3. **Agile ceremonies add value** — Sprint planning helps the whole team understand priorities and dependencies; it's not just a formality.

## Reflection

This week tested my patience and problem-solving skills. Debugging is a huge part of software development, and I'm more confident now in using browser DevTools and `console.log` strategically. Pair programming with a senior dev for 30 minutes was more valuable than hours of solo debugging.

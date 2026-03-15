# 📚 OJT Blog — My Internship Journey

A personal blog website built with **Nuxt 3**, **Tailwind CSS**, and **Nuxt Content** to document an On-the-Job Training (OJT) experience. Posts are written in Markdown and rendered with syntax highlighting — no database required.

[![Nuxt 3](https://img.shields.io/badge/Nuxt-3.x-00DC82?logo=nuxt.js&logoColor=white)](https://nuxt.com)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38bdf8?logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![Vue 3](https://img.shields.io/badge/Vue-3.x-42b883?logo=vue.js&logoColor=white)](https://vuejs.org)

---

## ✨ Features

| Feature | Details |
|---|---|
| 🏠 Homepage | Hero section, stats strip, latest posts, OJT timeline |
| 📝 Blog list | Searchable, sortable grid of all weekly posts |
| 📄 Post detail | Full Markdown content with syntax highlighting |
| 🖼️ Image gallery | Lightbox gallery per post with keyboard navigation |
| ⬅️ ➡️ Navigation | Previous / next post links |
| 📱 Responsive | Mobile-first layout via Tailwind CSS |
| 🧭 About page | Internship overview, tech stack, goals |
| 🎨 Theming | Custom brand colours & typography via Tailwind config |

---

## 🗂️ Repository Structure

```
ojt-blog/
├── app.vue                  # Root component
├── nuxt.config.ts           # Nuxt configuration
├── tailwind.config.js       # Tailwind CSS theme
├── assets/
│   └── css/
│       └── main.css         # Global styles & Tailwind layers
├── components/
│   └── PostCard.vue         # Reusable blog post card
├── content/
│   └── blog/                # ← Weekly Markdown blog entries
│       ├── week-01.md
│       ├── week-02.md
│       └── week-03.md
├── layouts/
│   └── default.vue          # Main layout (header + footer)
├── pages/
│   ├── index.vue            # Homepage
│   ├── about.vue            # About page
│   └── blog/
│       ├── index.vue        # Blog list page
│       └── [slug].vue       # Individual post page
└── public/
    └── images/              # Static images referenced in posts
```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** v18 or higher
- **npm** v9 or higher (or `pnpm` / `yarn`)

### 1. Install Dependencies

```bash
npm install
```

### 2. Run in Development Mode

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### 3. Build for Production

```bash
npm run build
npm run preview   # Preview the production build locally
```

### 4. Generate Static Site (for GitHub Pages)

```bash
npm run generate
```

This outputs a fully static site to the `.output/public/` directory.

---

## ✍️ Adding a New Weekly Blog Post

1. **Create a new Markdown file** in `content/blog/`:

   ```bash
   touch content/blog/week-04.md
   ```

2. **Add the front matter** at the top of the file:

   ```markdown
   ---
   title: "Your Post Title Here"
   week: 4
   date: "January 27, 2025"
   description: "A short one-line summary shown on the blog list."
   focus: "Topic Focus (e.g. Testing)"
   readTime: 5
   tags:
     - tag-one
     - tag-two
   coverImage: /images/week4-cover.jpg
   images:
     - src: /images/week4-photo1.jpg
       alt: Caption for the photo
   ---
   ```

3. **Write your post content** below the front matter in standard Markdown.

4. **Add your images** to the `public/images/` folder so they're served as static assets.

5. **Preview** your new post at `http://localhost:3000/blog/week-04`.

### Front Matter Reference

| Field | Type | Required | Description |
|---|---|---|---|
| `title` | `string` | ✅ | Post title |
| `week` | `number` | ✅ | Week number (used for ordering) |
| `date` | `string` | ✅ | Human-readable date |
| `description` | `string` | ✅ | Short summary (shown in cards) |
| `focus` | `string` | ❌ | Main topic of the week |
| `readTime` | `number` | ❌ | Estimated read time in minutes |
| `tags` | `string[]` | ❌ | Tags for filtering |
| `coverImage` | `string` | ❌ | Path to hero image |
| `images` | `{src, alt}[]` | ❌ | Gallery images |

---

## 🌐 Deployment

### GitHub Pages (Static)

1. Generate the static site:
   ```bash
   npm run generate
   ```

2. Deploy the `.output/public/` folder to the `gh-pages` branch using [gh-pages](https://www.npmjs.com/package/gh-pages) or a GitHub Actions workflow.

   Example GitHub Actions workflow (`.github/workflows/deploy.yml`):
   ```yaml
   name: Deploy to GitHub Pages
   on:
     push:
       branches: [main]
   jobs:
     deploy:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - uses: actions/setup-node@v4
           with:
             node-version: 20
         - run: npm ci
         - run: npm run generate
         - uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: .output/public
   ```

### VPS / Node Server

1. Build the project:
   ```bash
   npm run build
   ```

2. Start the server:
   ```bash
   node .output/server/index.mjs
   ```

   Or use PM2 for process management:
   ```bash
   pm2 start .output/server/index.mjs --name ojt-blog
   ```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| [Nuxt 3](https://nuxt.com) | Full-stack Vue 3 framework |
| [Vue 3](https://vuejs.org) | UI framework with Composition API |
| [Nuxt Content](https://content.nuxt.com) | Markdown-driven content layer |
| [Tailwind CSS](https://tailwindcss.com) | Utility-first CSS framework |
| [@tailwindcss/typography](https://tailwindcss.com/docs/typography-plugin) | Prose/article typography styles |

---

## 📄 License

This project is for personal/educational use as part of an OJT program. Feel free to fork and adapt it for your own internship journal.

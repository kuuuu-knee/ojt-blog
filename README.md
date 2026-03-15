# 📝 OJT Blog — My Internship Journey

A personal blog website built with **Nuxt 3**, **Tailwind CSS**, and **Markdown** to document my On-the-Job Training (OJT) experience week by week.

---

## ✨ Features

- 📅 **Weekly blog posts** written in Markdown
- 🖼️ **Image gallery** with lightbox viewer per post
- 🗓️ **Timeline view** of all entries
- 📱 **Fully responsive** mobile-first design
- ⚡ **Static site generation** — deployable to GitHub Pages or any VPS
- 🎨 **Clean modern UI** powered by Tailwind CSS

---

## 🗂️ Project Structure

```
ojt-blog/
├── assets/
│   ├── css/
│   │   └── tailwind.css       # Global Tailwind styles & custom components
│   └── images/                # Source images (optional)
├── components/
│   ├── BlogCard.vue            # Card component for blog post previews
│   ├── ImageGallery.vue        # Photo gallery with lightbox
│   ├── TheFooter.vue           # Site footer
│   └── TheHeader.vue           # Sticky navigation header
├── content/
│   └── posts/                 # Weekly blog posts (Markdown files)
│       ├── week-01.md
│       ├── week-02.md
│       └── week-03.md
├── layouts/
│   └── default.vue            # Main site layout (header + content + footer)
├── pages/
│   ├── index.vue              # Homepage with hero and recent posts
│   ├── about.vue              # About page
│   └── blog/
│       ├── index.vue          # Blog listing with timeline
│       └── [slug].vue         # Individual post page
├── public/
│   ├── favicon.svg
│   └── images/               # Uploaded photos for blog posts
├── nuxt.config.ts
├── tailwind.config.js
└── package.json
```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** v18 or higher
- **npm** v8 or higher

### Install Dependencies

```bash
npm install
```

### Run Locally

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## ✍️ Adding a New Weekly Blog Post

1. Create a new Markdown file in `content/posts/`:

   ```
   content/posts/week-04.md
   ```

2. Add the frontmatter header and your content:

   ```markdown
   ---
   week: 4
   title: "Your Post Title Here"
   date: "2025-01-27"
   description: "A short summary shown in the blog list."
   coverImage: "/images/week4-cover.jpg"
   images:
     - src: "/images/week4-photo1.jpg"
       alt: "Description of the photo"
       caption: "Optional caption"
   ---

   ## Overview

   Write your weekly update here using Markdown...

   ## Tasks Performed

   - Task 1
   - Task 2

   ## Challenges Encountered

   Describe any difficulties you faced.

   ## Lessons Learned

   What did you take away from this week?

   ## Reflection

   Personal thoughts and feelings about the week.
   ```

3. Add any photos to `public/images/` and reference them in the frontmatter or body.

4. The post will automatically appear on the blog list and homepage.

---

## 🖼️ Adding Images

- Place images in the `public/images/` directory.
- Reference them with an absolute path: `/images/my-photo.jpg`
- Images can be added:
  - As a `coverImage` in the frontmatter (shown as header image)
  - In the `images` array in frontmatter (shown in the gallery)
  - Inline in the Markdown body with `![alt text](/images/photo.jpg)`

---

## 🚢 Deployment

### GitHub Pages

1. Set `baseURL` in `nuxt.config.ts` to your repository name:

   ```ts
   app: {
     baseURL: '/ojt-blog/'
   }
   ```

2. Generate the static site:

   ```bash
   npm run generate
   ```

3. Deploy the `.output/public` folder to the `gh-pages` branch using [`gh-pages`](https://www.npmjs.com/package/gh-pages):

   ```bash
   npx gh-pages -d .output/public
   ```

### VPS / Any Static Host

```bash
npm run generate
# Upload the .output/public/ directory to your server
```

### Vercel / Netlify

Connect your GitHub repository and set the build command to `npm run generate` and the output directory to `.output/public`.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| [Nuxt 3](https://nuxt.com) | Vue 3 framework & SSG |
| [Tailwind CSS](https://tailwindcss.com) | Utility-first styling |
| [@nuxt/content](https://content.nuxt.com) | Markdown-based blog posts |
| [@tailwindcss/typography](https://tailwindcss.com/docs/typography-plugin) | Prose styling for post content |

---

## 📄 License

MIT — feel free to use this as a template for your own OJT blog!

# ojt-blog

A blog application built with [Next.js](https://nextjs.org), [TypeScript](https://www.typescriptlang.org/), and [Tailwind CSS](https://tailwindcss.com/).

## Prerequisites

Make sure you have the following installed on your machine:

- [Node.js](https://nodejs.org/) v18 or higher
- [npm](https://www.npmjs.com/) (comes with Node.js)

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to see the app.

The page auto-updates as you edit files under `src/`.

## Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start the development server at http://localhost:3000 |
| `npm run build` | Build the app for production |
| `npm run start` | Start the production server (run `build` first) |
| `npm run lint` | Lint the source files with ESLint |

## Project Structure

```
ojt-blog/
├── public/          # Static assets (images, icons, etc.)
├── src/
│   └── app/         # Next.js App Router pages and layouts
│       ├── layout.tsx
│       └── page.tsx
├── next.config.ts   # Next.js configuration
├── tailwind.config  # Tailwind CSS configuration (via postcss.config.mjs)
├── tsconfig.json    # TypeScript configuration
└── package.json
```

## Learn More

- [Next.js Documentation](https://nextjs.org/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)

## Deployment

The easiest way to deploy this app is with [Vercel](https://vercel.com/):

1. Push your code to GitHub.
2. Import the repository at [vercel.com/new](https://vercel.com/new).
3. Vercel will detect Next.js and configure the build automatically.

See the [Next.js deployment docs](https://nextjs.org/docs/app/building-your-application/deploying) for other options.
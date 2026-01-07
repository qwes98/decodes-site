# Decodes Site - Development Context

## Project Overview

**Tech Stack**: Next.js + TypeScript + Tailwind CSS + Contentlayer + MDX

**Template Base**: Tailwind Next.js Starter Blog
- Next.js App Directory (React Server Components)
- Contentlayer for markdown content management
- Pliny integration for analytics/comments/newsletter

## Project Structure

```
├── app/                    # Next.js pages & layouts
├── components/            # React components
├── data/
│   ├── blog/             # Blog posts (MDX/MD)
│   ├── authors/          # Author info
│   ├── siteMetadata.js   # Site config (MUST customize)
│   ├── headerNavLinks.ts # Navigation links
│   └── projectsData.ts   # Projects page data
├── layouts/              # Post layouts (PostLayout, PostSimple, PostBanner)
├── public/static/        # Images, favicons, assets
├── css/
│   ├── tailwind.css      # Tailwind config
│   └── prism.css         # Code block styles
├── contentlayer.config.ts # Content schema & MDX plugins
└── next.config.js        # Next.js config (CSP, image domains)
```

## Development Workflow

```bash
# Install
yarn

# Development server (http://localhost:3000)
yarn dev

# Production build
yarn build

# Static export (for GitHub Pages/S3)
EXPORT=1 UNOPTIMIZED=1 yarn build
# With base path: EXPORT=1 UNOPTIMIZED=1 BASE_PATH=/myblog yarn build
```

## Key Customization Points

1. **Site Metadata**: `data/siteMetadata.js` - site title, description, URLs
2. **Navigation**: `data/headerNavLinks.ts` - header menu links
3. **Author Info**: `data/authors/default.md` - main author (required)
4. **Projects**: `data/projectsData.ts` - projects page content
5. **Blog Posts**: `data/blog/` - add MDX/MD files
6. **Logo**: `data/logo.svg` - replace with custom logo
7. **Styling**: `tailwind.config.js` + `css/tailwind.css` - theme customization
8. **MDX Components**: `components/MDXComponents.js` - custom React components in MDX

## Content Format (Frontmatter)

```yaml
---
title: 'Post Title' (required)
date: '2021-01-12' (required)
tags: ['next-js', 'tailwind'] (optional)
draft: false (optional)
summary: 'Brief description' (optional)
images: ['/static/images/cover.jpg'] (optional)
authors: ['default'] (optional, uses default if not specified)
layout: PostLayout (optional, default: PostLayout)
---
```

## Important Config Files

- **next.config.js**: CSP policy, image optimization, base path
- **contentlayer.config.ts**: Content schema, MDX plugins (rehype/remark)
- **tailwind.config.js**: Theme, colors, fonts, primary color
- **app/layout.tsx**: Root layout with metadata

## Deployment Notes

- **Vercel**: Zero config deployment (recommended)
- **Static hosting**: Use `EXPORT=1 UNOPTIMIZED=1` build
  - Remove `headers()` from next.config.js
  - Remove `api` folder if unused
- **Base path**: Set `BASE_PATH` env var for subdirectory deployments

## Features to Note

- Server-side syntax highlighting (rehype-prism-plus)
- Math support (KaTeX)
- Citation support (rehype-citation)
- Image optimization (next/image)
- Multiple blog layouts (PostLayout, PostSimple, PostBanner)
- SEO: RSS, sitemaps, structured data
- Analytics options via Pliny
- Comment systems via Pliny (Giscus, Utterances, Disqus)

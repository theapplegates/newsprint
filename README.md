# Newsprint

A newspaper-style blog built with [Eleventy (11ty)](https://www.11ty.dev/) that embraces a classic newspaper aesthetic while functioning as a newsletter-first publication.

## Features

- **Newspaper Design** — Multi-column layouts, traditional masthead, drop caps, pull quotes, ruled lines, grayscale palette
- **Newsletter-First RSS** — Full-content Atom feeds with email-safe HTML, plus category-specific feeds
- **Responsive** — Mobile-first design that gracefully collapses columns on smaller screens
- **Accessible** — Semantic HTML, proper heading hierarchy, skip links, ARIA labels
- **Print-Ready** — Dedicated print stylesheet
- **Fast** — Static HTML, lazy-loaded images, optimized web fonts

## Quick Start

```bash
# Install dependencies
npm install

# Start development server
npm start

# Build for production
npm run build
```

The dev server runs at `http://localhost:8080`.

## Project Structure

```
src/
├── _data/          # Site metadata and navigation
├── _includes/
│   ├── layouts/    # Page layouts (base, home, article, archive)
│   ├── components/ # Reusable components (masthead, footer, sidebar, etc.)
│   └── partials/   # Head, scripts
├── articles/       # Blog posts (Markdown)
├── pages/          # Static pages and category pages
├── css/            # Newspaper-style CSS architecture
│   ├── base/       # Variables, reset, typography
│   ├── components/ # Masthead, article, sidebar, footer styles
│   └── layouts/    # Homepage, article page, archive styles
├── feed.njk        # Main Atom feed
└── index.njk       # Homepage
```

## Writing Articles

Create a new `.md` file in `src/articles/`:

```yaml
---
title: "Article Headline"
subtitle: "Optional deck/subheading"
date: 2026-02-06
author: "Writer Name"
category: "News"       # News, Opinion, Features, Culture, Business
featured: true         # Show in featured section on homepage
excerpt: "Article summary for RSS and meta"
---

Article content in Markdown...
```

## RSS Feeds

- **All articles:** `/feed.xml`
- **News:** `/feed/news.xml`
- **Opinion:** `/feed/opinion.xml`
- **Features:** `/feed/features.xml`

## License

MIT

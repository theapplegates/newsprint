# Newsprint: a Newspaper-Style Blog Specification
## 11ty Publication with Newsletter-First RSS

---

## Project Overview

A modern blog built with 11ty (Eleventy) that embraces a classic newspaper aesthetic while functioning as a newsletter-first publication. The design prioritizes readability, traditional typography, and excellent RSS feed implementation for email newsletter distribution.

---

## Design Requirements

### Visual Aesthetic

**Newspaper Elements:**
- Multi-column layout for article content (2-3 columns on desktop)
- Traditional newspaper masthead with publication name, date, and tagline
- Section headers styled as newspaper departments (Opinion, Features, News, etc.)
- Ruled lines separating articles and sections
- Grayscale color scheme with newsprint texture option
- Pull quotes and drop caps for visual interest
- Bylines and datelines in traditional newspaper format

**Typography:**
- **Masthead/Logo:** Playfair Display or similar serif (bold, large)
- **Headlines:** Playfair Display or Libre Baskerville (hierarchical sizing)
- **Subheadings:** Georgia or Merriweather (medium weight)
- **Body Text:** Georgia, Merriweather, or Droid Serif (16-18px, justified)
- **Captions/Metadata:** Smaller serif or sans-serif (14px)
- Tight leading (line-height: 1.4-1.5) for newspaper density
- Proper widow/orphan control

**Layout Principles:**
- Masonry/grid layout for article previews on homepage
- Different-sized article blocks (feature stories larger, briefs smaller)
- Traditional newspaper fold concept (important content above the fold)
- Sidebar for "quick hits" or smaller news items
- Weather widget/date stamp in corner
- Print-friendly styles

---

## Technical Stack

### Core Technology
- **Static Site Generator:** 11ty (Eleventy)
- **Templating:** Nunjucks (or Liquid)
- **CSS Framework:** Custom CSS based on Tufte CSS principles + newspaper modifications
- **Build Tool:** 11ty native build
- **Deployment:** Netlify, Vercel, or GitHub Pages

### CSS Architecture

```
styles/
├── base/
│   ├── reset.css
│   ├── typography.css
│   └── variables.css
├── components/
│   ├── masthead.css
│   ├── article.css
│   ├── columns.css
│   ├── sidebar.css
│   └── footer.css
├── layouts/
│   ├── homepage.css
│   ├── article-page.css
│   └── archive.css
└── newspaper.css (main import file)
```

**Key CSS Features:**
- CSS Grid for overall layout
- CSS Multi-column for article text (`column-count`, `column-gap`, `column-rule`)
- CSS custom properties for theme variables
- Print stylesheet included
- Mobile-first responsive (columns collapse on mobile)

---

## Content Structure

### Content Types

**1. Articles/Posts**
```yaml
# Front matter structure
---
title: "Article Headline"
subtitle: "Optional deck/subheading"
date: 2026-02-06
author: "Writer Name"
category: "News" # or Opinion, Features, Culture, etc.
featured: true # for homepage feature placement
image: /img/article-image.jpg
imageCaption: "Photo caption here"
excerpt: "Article summary for RSS and meta"
---
```

**2. Sections/Categories**
- News
- Opinion
- Features
- Culture
- Business
- Etc. (customizable)

**3. Special Features**
- Photo essays (image-heavy layouts)
- Interviews (Q&A format)
- Long-form features (single-column option)
- "Briefs" section (short news items)

### File Structure

```
project-root/
├── src/
│   ├── _data/
│   │   ├── site.json (metadata, masthead text)
│   │   └── navigation.json
│   ├── _includes/
│   │   ├── layouts/
│   │   │   ├── base.njk
│   │   │   ├── home.njk
│   │   │   ├── article.njk
│   │   │   └── archive.njk
│   │   ├── components/
│   │   │   ├── masthead.njk
│   │   │   ├── article-card.njk
│   │   │   ├── sidebar.njk
│   │   │   └── footer.njk
│   │   └── partials/
│   │       ├── head.njk
│   │       └── scripts.njk
│   ├── articles/
│   │   └── *.md (all blog posts)
│   ├── pages/
│   │   ├── about.md
│   │   └── archive.md
│   ├── css/
│   └── img/
├── .eleventy.js
└── package.json
```

---

## RSS/Newsletter Features

### RSS Feed Requirements

**Primary Full-Content Feed** (`/feed.xml`)
- Complete article HTML included
- Properly formatted for email clients
- Images embedded with absolute URLs
- Styled inline CSS for email rendering
- All categories included

**Category-Specific Feeds**
- `/feed/news.xml`
- `/feed/opinion.xml`
- `/feed/features.xml`
- (One per category)

**Feed Metadata:**
```xml
<title>Publication Name</title>
<description>Newsletter description</description>
<link>https://yoursite.com</link>
<language>en-us</language>
<copyright>Copyright info</copyright>
<managingEditor>editor@email.com</managingEditor>
<webMaster>webmaster@email.com</webMaster>
<pubDate>Auto-generated</pubDate>
<lastBuildDate>Auto-generated</lastBuildDate>
<image>Publication logo</image>
```

**Item Structure:**
```xml
<item>
  <title>Article Title</title>
  <link>Permalink</link>
  <description>Full article HTML with inline styles</description>
  <author>Author email/name</author>
  <category>Section</category>
  <pubDate>RFC 822 date</pubDate>
  <guid isPermaLink="true">Permalink</guid>
  <enclosure> (if image featured)
</item>
```

### Newsletter Optimization

**Email-Friendly HTML:**
- Inline CSS (no external stylesheets)
- Table-based layouts for email client compatibility
- Simplified newspaper styling for email
- Alt text for all images
- Plain text fallback version

**11ty RSS Plugin Configuration:**
```javascript
// .eleventy.js
const pluginRss = require("@11ty/eleventy-plugin-rss");

module.exports = function(eleventyConfig) {
  eleventyConfig.addPlugin(pluginRss);
  
  // Custom filter for email-safe HTML
  eleventyConfig.addFilter("emailSafe", function(content) {
    // Inline styles, absolute URLs, etc.
  });
};
```

**Newsletter Distribution Options:**
- Direct RSS-to-email services (Substack, Buttondown, Kill the Newsletter)
- Self-hosted (Listmonk, Mailtrain)
- RSS readers that support email notifications
- Social media auto-posting from RSS

---

## Key Features

### Homepage Layout

**Masthead Section:**
- Publication name (large, centered or left-aligned)
- Date and edition info (e.g., "Friday, February 6, 2026 | Vol. 1, No. 42")
- Tagline/mission statement
- Weather widget (optional)
- Navigation menu (styled as newspaper sections)

**Featured Article:**
- Large hero placement above the fold
- Prominent headline (h1)
- Featured image
- Article excerpt
- "Continue reading" link

**Grid Layout:**
- 3-column grid on desktop
- Mix of article sizes (1x1, 2x1, 1x2 blocks)
- Category labels on each article
- Thumbnail images
- Bylines and dates
- Excerpt snippets

**Sidebar:**
- "In This Issue" table of contents
- Recent articles list
- Newsletter signup form
- RSS feed links
- Social media links

### Article Page Layout

**Article Header:**
- Section/category label
- Headline (h1)
- Subtitle/deck (h2, if present)
- Byline and date
- Estimated read time
- Social sharing buttons

**Article Body:**
- Multi-column layout (2-3 columns on desktop)
- Drop cap for first paragraph
- Pull quotes styled as newspaper blockquotes
- Inline images with captions
- Horizontal rules between sections
- Related articles footer

**Article Footer:**
- Author bio box
- Related/recommended articles
- Newsletter signup CTA
- Comments section (optional)

### Archive/Section Pages

- Chronological or categorical listing
- Newspaper-style headlines list
- Date organization
- Pagination
- Filter by category/tag

---

## Performance & SEO

### Optimization
- Lazy loading for images
- Minified CSS/JS
- Static HTML (fast by default with 11ty)
- Responsive images with `<picture>` element
- Web fonts optimized with `font-display: swap`

### SEO/Meta
- Open Graph tags for social sharing
- Twitter Card metadata
- Structured data (Schema.org Article)
- Semantic HTML5
- Descriptive alt text
- XML sitemap
- robots.txt

---

## Additional Features

### Nice-to-Haves
- Dark mode toggle (inverted newspaper look)
- "Print Edition" view (optimized for printing)
- Search functionality
- Tag system
- Series/serialized content support
- Guest author system
- Editorial calendar display
- Corrections/updates log

### Accessibility
- Proper heading hierarchy
- ARIA labels where needed
- Keyboard navigation
- Sufficient color contrast
- Responsive font sizing
- Skip to content link
- Alt text for all images

---

## Implementation Phases

### Phase 1: Core Setup
1. Install 11ty and basic configuration
2. Set up file structure
3. Create base layout and templates
4. Implement basic typography

### Phase 2: Newspaper Styling
1. Build masthead component
2. Implement multi-column CSS
3. Create article card component
4. Style homepage grid layout
5. Design article page layout

### Phase 3: RSS/Newsletter
1. Configure RSS plugin
2. Create feed templates (main + category feeds)
3. Build email-safe HTML filter
4. Add newsletter signup forms
5. Test in email clients

### Phase 4: Content & Polish
1. Add sample articles
2. Create archive/section pages
3. Implement search
4. Add social sharing
5. Performance optimization
6. Accessibility audit

---

## RSS Feed Technical Specifications

### Feed Generation (11ty)

Create `src/feed.njk`:
```njk
---
permalink: /feed.xml
excludeFromSitemap: true
---
<?xml version="1.0" encoding="utf-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
  <title>{{ site.title }}</title>
  <subtitle>{{ site.description }}</subtitle>
  <link href="{{ site.url }}/feed.xml" rel="self"/>
  <link href="{{ site.url }}"/>
  <updated>{{ collections.articles | rssLastUpdatedDate }}</updated>
  <id>{{ site.url }}/</id>
  <author>
    <name>{{ site.author }}</name>
    <email>{{ site.email }}</email>
  </author>
  {% for article in collections.articles | reverse | limit(20) %}
  <entry>
    <title>{{ article.data.title }}</title>
    <link href="{{ site.url }}{{ article.url }}"/>
    <updated>{{ article.date | rssDate }}</updated>
    <id>{{ site.url }}{{ article.url }}</id>
    <content type="html">
      {{ article.templateContent | htmlToAbsoluteUrls(site.url) | emailSafe }}
    </content>
  </entry>
  {% endfor %}
</feed>
```

### Email-Safe Content Filter

Key transformations needed:
- Convert relative URLs to absolute
- Inline CSS styles
- Optimize image tags for email
- Strip unsupported HTML/CSS
- Add table-based layout wrapper for email clients

---

## Example Configuration

### site.json
```json
{
  "title": "The Daily Chronicle",
  "description": "A newsletter-first publication covering tech, culture, and ideas",
  "url": "https://dailychronicle.com",
  "author": "Editorial Team",
  "email": "editor@dailychronicle.com",
  "masthead": {
    "tagline": "All the News That's Fit to Ship",
    "established": "2026"
  }
}
```

### .eleventy.js (key configurations)
```javascript
module.exports = function(eleventyConfig) {
  // RSS Plugin
  const pluginRss = require("@11ty/eleventy-plugin-rss");
  eleventyConfig.addPlugin(pluginRss);
  
  // Collections
  eleventyConfig.addCollection("articles", function(collection) {
    return collection.getFilteredByGlob("src/articles/**/*.md");
  });
  
  // Pass through
  eleventyConfig.addPassthroughCopy("src/css");
  eleventyConfig.addPassthroughCopy("src/img");
  
  return {
    dir: {
      input: "src",
      output: "_site"
    }
  };
};
```

---

## Resources & Inspiration

- **Tufte CSS:** https://edwardtufte.github.io/tufte-css/
- **Newspaper CodePen:** https://codepen.io/silkine/pen/QWBxVX
- **CSS Multi-column:** MDN Web Docs
- **11ty RSS Plugin:** https://www.11ty.dev/docs/plugins/rss/
- **Email on Acid:** For testing email rendering
- **Schema.org Article:** For structured data

---

## Success Metrics

- RSS feed validates with W3C Feed Validator
- Email renders correctly in major clients (Gmail, Outlook, Apple Mail, etc.)
- Page load time < 2 seconds
- Lighthouse score > 90
- Mobile responsive on all breakpoints
- WCAG 2.1 AA accessibility compliance
- Newsletter signup conversion rate tracking

---

*Specification Document v1.0 - Ready for Implementation*
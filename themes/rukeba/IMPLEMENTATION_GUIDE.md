# Rukeba Theme - Implementation Guide

## Overview

This document provides a complete guide to the newly created Hugo theme for rukeba.com. All template files have been created and are ready to use with the Hugo static site generator.

## Files Created

### Layouts (14 files)

#### Base Layout
- `layouts/_default/baseof.html` - Main template wrapper with HTML structure, head, header, content, footer

#### Page Templates
- `layouts/index.html` - Homepage
- `layouts/_default/single.html` - Individual post pages (blog and songbook)
- `layouts/by-the-way/list.html` - Blog listing with pagination (10 per page)
- `layouts/by-the-way/all.html` - All blog posts with tag sidebar
- `layouts/songbook/list.html` - Songbook listing with pagination (10 per page)
- `layouts/songbook/all.html` - All songbook posts with artist sidebar
- `layouts/taxonomy/tag.html` - Tag archive pages

#### Partials (6 files)
- `layouts/partials/head.html` - HTML head with meta tags, Bootstrap, Font Awesome, custom CSS
- `layouts/partials/header.html` - Site header with logo and navigation
- `layouts/partials/footer.html` - Site footer with social links
- `layouts/partials/google-analytics.html` - GA4 tracking code
- `layouts/partials/custom-css.html` - Placeholder for custom CSS
- `layouts/partials/custom-scripts.html` - jQuery, Bootstrap JS, LazyLoad, custom JS

### Static Files
- `static/css/rukeba.css` - Theme custom CSS
- `static/js/rukeba.js` - Theme custom JavaScript

### Configuration
- `theme.toml` - Hugo theme metadata

### Documentation
- `README.md` - Complete theme documentation

## Features Implemented

✅ **Hugo Template Syntax** - All files use Hugo template language (not Jekyll Liquid)
✅ **Russian Language** - Navigation and UI strings in Russian
✅ **Bootstrap 3.3.7** - Responsive CSS framework via CDN
✅ **Date Format** - Configurable format: "2 Jan 2006, 15:04"
✅ **Tag Support** - Per-section tag system with dedicated tag pages
✅ **Pagination** - Built-in pagination for list pages (10 items per page)
✅ **Section-Specific Filtering** - Tags organized by section (/by-the-way/tags/ and /songbook/tags/)
✅ **Responsive Design** - Bootstrap grid system for mobile-friendly layout
✅ **RSS Feeds** - Automatic feed generation for all sections
✅ **Google Analytics** - GA4 integration (optional)

## Directory Structure

```
themes/rukeba/
├── README.md                          # Theme documentation
├── theme.toml                         # Theme metadata
├── layouts/
│   ├── _default/
│   │   ├── baseof.html               # Base template
│   │   └── single.html               # Single post template
│   ├── index.html                    # Homepage
│   ├── by-the-way/
│   │   ├── list.html                 # Blog listing (10 posts)
│   │   └── all.html                  # All blog posts
│   ├── songbook/
│   │   ├── list.html                 # Songbook listing (10 posts)
│   │   └── all.html                  # All songbook posts
│   ├── taxonomy/
│   │   └── tag.html                  # Tag pages
│   └── partials/
│       ├── head.html                 # HTML head
│       ├── header.html               # Site header
│       ├── footer.html               # Site footer
│       ├── google-analytics.html     # GA tracking
│       ├── custom-css.html           # Custom CSS placeholder
│       └── custom-scripts.html       # Custom scripts & libraries
└── static/
    ├── css/
    │   └── rukeba.css                # Custom theme CSS
    └── js/
        └── rukeba.js                 # Custom theme JavaScript
```

## Usage Instructions

### 1. Ensure Hugo Configuration is Correct

Your `hugo.toml` should have:

```toml
baseURL = 'http://rukeba.com'
languageCode = 'ru-RU'
defaultContentLanguage = 'ru'
title = 'rukeba.com'
theme = 'rukeba'

[params]
  description = 'Блог, песенник и ссылки, которые ведёт rukeba.'
  dateFormat = '2 Jan 2006, 15:04'
  cdnUrl = 'https://rukeba.com'
  logo = 'https://rukeba.com/assets/img/r.png'
  googleAnalytics = 'UA-1638627-8'

[taxonomies]
  tag = 'tags'
  category = 'categories'

[outputs]
  home = ['HTML', 'RSS']
  section = ['HTML', 'RSS']
  taxonomy = ['HTML']
  term = ['HTML']

[permalinks]
  'by-the-way' = '/:section/:slug/'
  'songbook' = '/:section/:slug/'
```

### 2. Organize Content

```
content/
├── _index.md                    # Homepage content
├── by-the-way/
│   ├── _index.md               # By-the-way section index
│   └── YYYY-MM-DD-slug.md      # Blog posts
└── songbook/
    ├── _index.md               # Songbook section index
    └── YYYY-MM-DD-slug.md      # Songbook entries
```

### 3. Content Front Matter Format

For **by-the-way** posts:
```yaml
---
title: 'Post Title'
date: 2006-12-14 19:20:00 +0300
tags: ["tag1", "tag2"]
---
Content here...
```

For **songbook** posts:
```yaml
---
title: 'Artist / Song Title'
date: 2008-01-16 00:59:00 +0300
tags: ["Artist Name"]
---
Content here...
```

### 4. Build and Serve

```bash
# Build the site
hugo

# Serve locally with hot reload
hugo server

# Build for production
hugo --minify
```

## Template Breakdown

### baseof.html
- Root template wrapping all pages
- Includes: head, header, main content block, footer
- Conditionally includes Google Analytics

### Single Post (single.html)
- Displays: Title, date, tags, full content
- CSS classes: `.post`, `.post-full`
- Links tags to section-specific tag pages

### Homepage (index.html)
- Simple wrapper for homepage content
- Content comes from `content/_index.md`
- CSS class: `#home`

### By-the-Way List (list.html)
- Shows latest 10 blog posts
- Each post shows: title, date, tags, excerpt
- Includes pagination links
- CSS class: `.by-the-way`
- Posts ordered by date (newest first)

### By-the-Way All (all.html)
- Two-column layout: 8-column content, 4-column sidebar
- Lists all blog posts (no pagination)
- Sidebar shows all unique tags
- CSS class: `.by-the-way`
- Uses Bootstrap grid: `col-md-8` and `col-md-4`

### Songbook List (list.html)
- Shows latest 10 songbook entries
- Each entry shows: title, date, tags, full content
- Includes pagination links
- CSS class: `.songbook`
- Posts ordered by date (newest first)

### Songbook All (all.html)
- Two-column layout: 8-column content, 4-column sidebar
- Lists all songbook entries (no pagination)
- Sidebar shows all unique artists/tags
- CSS class: `.songbook`
- Uses Bootstrap grid: `col-md-8` and `col-md-4`

### Tag Pages (tag.html)
- Displays all posts with a specific tag
- Shows: title, date, tags, excerpt
- Works for both sections (automatically routed)
- URLs: `/by-the-way/tags/{tag}/` and `/songbook/tags/{tag}/`

### Partials

**head.html**
- Meta tags: charset, viewport, OG tags
- Bootstrap CSS 3.3.7 (CDN)
- Font Awesome 4.7 (CDN)
- Custom CSS file
- RSS feed link
- Favicon link

**header.html**
- Brand/logo with link to homepage
- Navigation menu with Bootstrap grid
- Navigation items: Home, По жизни, Песенник, + custom menu items
- Uses Bootstrap classes: `.row`, `.col-md-12`

**footer.html**
- Copyright notice
- Social links: RSS, Email, GitHub, Twitter
- Attribution to Hugo
- Responsive with Bootstrap

**google-analytics.html**
- GA4 script tag
- Only renders if `googleAnalytics` parameter is set
- Uses gtag() function

**custom-css.html**
- Placeholder for additional CSS
- Can be populated via `customCSS` site parameter
- Wrapped in `<style>` tags

**custom-scripts.html**
- jQuery 1.12.4 (CDN)
- Bootstrap 3.3.7 JS (CDN)
- LazyLoad 2.4.0 (CDN)
- Custom `rukeba.js`
- Placeholder for additional JavaScript

## Styling

### CSS Cascade
1. Bootstrap 3.3.7 (base styles)
2. Font Awesome 4.7 (icons)
3. Custom rukeba.css (theme styles)
4. Optional custom CSS from config

### Key CSS Classes Used
- `.container` - Bootstrap container
- `.row` - Bootstrap row
- `.col-md-8`, `.col-md-4` - Bootstrap columns
- `.post` - Post content styling
- `.post-title` - Post title styling
- `.post-meta` - Date and tag styling
- `.post-excerpt` - Excerpt styling
- `.by-the-way` - Blog section styling
- `.songbook` - Songbook section styling
- `.pagination` - Pagination styling
- `.tag` - Tag link styling
- `.sidebar` - Sidebar styling
- `.night` - Dark mode (add to body)

### Colors (from rukeba.css)
- Link color: #05C (blue)
- Visited link color: #909 (purple)
- Hover link color: #C00 (red)
- Active nav: rgba(0, 85, 204, 0.8)
- Brand background: #eee
- Footer border: #eee
- Footer text: #888

## Configuration Options (hugo.toml)

```toml
[params]
  # Required
  title = "Your Site Title"
  description = "Site description"
  
  # Optional
  dateFormat = "2 Jan 2006, 15:04"      # Date display format
  logo = "https://example.com/logo.png" # Logo URL
  googleAnalytics = "UA-XXXXXXXXX-X"    # Google Analytics ID
  email = "contact@example.com"         # Email for footer
  github = "username"                   # GitHub username
  twitter = "username"                  # Twitter handle
  customCSS = ""                        # Custom CSS as string
  customScripts = ""                    # Custom JS as string
```

## Custom Menu Items

Add custom navigation items to `hugo.toml`:

```toml
[[menu.main]]
  name = "About"
  url = "/about/"
  weight = 1

[[menu.main]]
  name = "Archive"
  url = "/archive/"
  weight = 2
```

## How Template Selection Works

Hugo automatically selects templates based on content location and type:

1. **Homepage** (`/`) → `layouts/index.html`
2. **By-the-way section posts** (`/by-the-way/*`) → `layouts/_default/single.html`
3. **By-the-way listing** (`/by-the-way/`) → `layouts/by-the-way/list.html`
4. **Songbook section posts** (`/songbook/*`) → `layouts/_default/single.html`
5. **Songbook listing** (`/songbook/`) → `layouts/songbook/list.html`
6. **Tag pages** (`/tags/{tag}/`) → `layouts/taxonomy/tag.html`

## Dynamic Features

### Pagination
- **By-the-way list**: Shows 10 most recent posts, with pagination for older posts
- **Songbook list**: Shows 10 most recent entries, with pagination for older entries
- **Pagination variables**: `$paginator.HasPrev`, `$paginator.HasNext`, `$paginator.TotalPages`, `$paginator.PageNumber`

### Tag Cloud
- **By-the-way all.html**: Sidebar generates list of all tags from blog posts
- **Songbook all.html**: Sidebar generates list of all artists/tags from songbook entries
- **Dynamic tag links**: Tags link to `/section/tags/{tag}/` pages

### Date Formatting
- All dates use `{{ .Date.Format .Site.Params.dateFormat }}`
- Default format: "2 Jan 2006, 15:04"
- Can be customized in `hugo.toml`

### Summary/Excerpt Generation
- Hugo automatically generates excerpts from post content
- Used in list pages: `{{ .Summary }}`
- Set `summaryLength` in `hugo.toml` to control excerpt length
- Current default: 70 words

## Next Steps

1. ✅ Theme files created
2. ✅ Configuration documented
3. **TODO**: Verify the site builds correctly
4. **TODO**: Create `content/_index.md` for homepage
5. **TODO**: Create `content/by-the-way/_index.md` for section
6. **TODO**: Create `content/songbook/_index.md` for section
7. **TODO**: Update any custom site parameters in `hugo.toml`
8. **TODO**: Test all pages locally with `hugo server`
9. **TODO**: Deploy to production

## Troubleshooting

### Page not rendering
- Check content file exists in correct directory
- Check front matter is valid YAML
- Run `hugo server` and check console for errors

### Styles not applying
- Clear browser cache (Ctrl+Shift+Delete or Cmd+Shift+Delete)
- Check Bootstrap CSS is loading (check Network tab in DevTools)
- Verify CSS file path in `head.html` is correct

### Tags not showing
- Ensure posts have `tags` field in front matter
- Check `[taxonomies]` configuration in `hugo.toml`
- Tag pages should be auto-generated at `/section/tags/{tag}/`

### Pagination not working
- Check `summaryLength` parameter is set in `hugo.toml`
- Verify page list templates use `.Paginate` function
- Check section has more than one page of content

## Support

For issues or questions about the theme, refer to the `README.md` file in the theme directory or the main project documentation.

---

**Theme Version**: 1.0  
**Created**: 2024  
**Hugo Minimum Version**: 0.87.0  
**License**: MIT

# Rukeba Hugo Theme

A clean, minimal Hugo theme for a blog with multiple content sections (blog posts and songbook).

## Features

- **Multiple Content Sections**: Support for "by-the-way" (blog) and "songbook" (lyrics) sections
- **Bootstrap 3.3.7**: Responsive design with Bootstrap CSS framework
- **Tag Support**: Tag-based organization per section
- **Pagination**: Built-in pagination for list pages
- **RSS Feed**: Automatic RSS feed generation
- **Responsive Design**: Mobile-friendly layout with Bootstrap grid system
- **Google Analytics**: Optional Google Analytics integration
- **Internationalization**: Russian language support (easily customizable)

## Content Structure

### Hugo Configuration (hugo.toml)

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
```

### Content Directory Structure

```
content/
├── _index.md              # Homepage content
├── by-the-way/            # Blog posts section
│   ├── _index.md
│   └── 2006-12-14-*.md
├── songbook/              # Songbook/lyrics section
│   ├── _index.md
│   └── 2008-01-16-*.md
└── tags/                  # Tag pages
```

### Post Front Matter Example

For **by-the-way** posts:
```yaml
---
title: 'Post Title'
slug: 'post-slug'
date: 2006-12-14 19:20:00 +0300
tags: ["tag1", "tag2"]
---
```

For **songbook** posts:
```yaml
---
title: 'Artist / Song Title'
slug: 'artist-song-slug'
date: 2008-01-16 00:59:00 +0300
tags: ["Artist Name"]
---
```

## Layout Structure

### Base Layout (`layouts/_default/baseof.html`)
The main template that wraps all pages:
- HTML structure
- Includes head, header, content area, footer
- Includes Google Analytics and custom scripts

### Page Layouts

1. **Homepage** (`layouts/index.html`)
   - Displays homepage content from `content/_index.md`
   - Custom CSS class: `#home`

2. **Single Post** (`layouts/_default/single.html`)
   - Template for individual blog and songbook posts
   - Displays: title, date, tags, full content
   - Custom CSS class: `.post-full`

3. **By-the-Way List** (`layouts/by-the-way/list.html`)
   - Displays latest 10 blog posts
   - Shows title, date, tags, and excerpt (summary)
   - Includes pagination
   - Custom CSS class: `.by-the-way`

4. **By-the-Way All** (`layouts/by-the-way/all.html`)
   - Displays all blog posts on one page
   - Includes sidebar with tag list
   - Two-column layout (8/4 split with Bootstrap)
   - Custom CSS class: `.by-the-way`

5. **Songbook List** (`layouts/songbook/list.html`)
   - Displays latest 10 songbook entries
   - Shows title, date, tags, and full content
   - Includes pagination
   - Custom CSS class: `.songbook`

6. **Songbook All** (`layouts/songbook/all.html`)
   - Displays all songbook entries on one page
   - Includes sidebar with artist list
   - Two-column layout (8/4 split with Bootstrap)
   - Custom CSS class: `.songbook`

7. **Tag Pages** (`layouts/taxonomy/tag.html`)
   - Displays all posts with a specific tag
   - Works for both sections (by-the-way and songbook)
   - Shows title, date, tags, and excerpt

### Partials

All partials are in `layouts/partials/`:

1. **head.html**
   - Meta tags (charset, viewport, OpenGraph, etc.)
   - Bootstrap CSS link
   - Font Awesome icon library
   - Custom CSS
   - Favicon
   - RSS feed link

2. **header.html**
   - Site logo/brand
   - Main navigation menu
   - Navigation items: Home, По жизни (By-the-Way), Песенник (Songbook)
   - Optional custom menu items from `menus.main`

3. **footer.html**
   - Copyright information
   - Social links (RSS, Email, GitHub, Twitter)
   - Powered by Hugo attribution

4. **google-analytics.html**
   - Google Analytics script (GA4)
   - Only renders if `googleAnalytics` param is set

5. **custom-css.html**
   - Placeholder for additional custom CSS
   - Can be populated via `customCSS` site param

6. **custom-scripts.html**
   - jQuery
   - Bootstrap JS
   - LazyLoad for images
   - Custom rukeba.js
   - Placeholder for additional scripts via `customScripts` param

## Styling

### CSS Files
- Bootstrap 3.3.7 (CDN)
- Font Awesome 4.7 (CDN)
- Custom theme CSS: `themes/rukeba/static/css/rukeba.css`

### Custom CSS (rukeba.css)
Features:
- Typography styling (16px base font)
- Link styling with custom colors and underlines
- Header and navigation styling
- Post and list item styling
- Gallery styling with lazy loading
- Embedded responsive media
- Ukrainian flag CSS (inline SVG)
- Night mode support (body.night class)
- Bootstrap integration

### JavaScript Files
- jQuery 1.12.4 (CDN)
- Bootstrap 3.3.7 JS (CDN)
- LazyLoad for image lazy loading
- Custom `rukeba.js` for:
  - Active menu item highlighting
  - Lazy image loading initialization

## Site Parameters (hugo.toml)

```toml
[params]
  description = 'Site description'
  dateFormat = '2 Jan 2006, 15:04'  # Hugo time format
  cdnUrl = 'https://example.com'
  logo = 'https://example.com/logo.png'
  googleAnalytics = 'UA-XXXXXXXXX-X'
  email = 'contact@example.com'
  github = 'username'
  twitter = 'username'
  customCSS = ''  # Optional custom CSS as string
  customScripts = ''  # Optional custom JavaScript as string
```

## Pagination Configuration

Add this to `hugo.toml` to customize pagination:

```toml
[pagination]
  disableAliases = false
  
[outputs]
  home = ['HTML', 'RSS']
  section = ['HTML', 'RSS']
  taxonomy = ['HTML']
  term = ['HTML']
```

## Date Format

Default date format: `2 Jan 2006, 15:04` (e.g., "25 Dec 2023, 15:30")

This format is set in `hugo.toml` and used throughout templates via `{{ .Date.Format .Site.Params.dateFormat }}`

## Language

All template text is in Russian. To customize:

1. Homepage title and descriptions in `content/_index.md`
2. Navigation labels in `layouts/partials/header.html`
3. UI strings in individual layout files

## Bootstrap Grid System

The theme uses Bootstrap 3.3.7 grid system:
- `.container` for main content wrapper
- `.row` for row containers
- `.col-md-8` and `.col-md-4` for two-column layouts
- Full responsive behavior for mobile devices

## RSS Feed

RSS feeds are automatically generated for:
- Homepage: `/feed/`
- By-the-way section: `/by-the-way/feed/`
- Songbook section: `/songbook/feed/`

## Tags and Taxonomies

The theme supports hierarchical tags per section:
- **By-the-way tags**: `/by-the-way/tags/[tag-slug]/`
- **Songbook tags**: `/songbook/tags/[artist-name]/`

Tag pages are generated automatically by Hugo using the `taxonomy/tag.html` template.

## Customization Guide

### Change Colors
Edit `themes/rukeba/static/css/rukeba.css`:
- `#05C` - Main link color (blue)
- `#909` - Visited link color (purple)
- `#C00` - Hover link color (red)

### Add Menu Items
Add to `hugo.toml`:
```toml
[[menu.main]]
  name = "About"
  url = "/about/"
  weight = 1
```

### Change Date Format
Update in `hugo.toml`:
```toml
[params]
  dateFormat = 'Jan 2, 2006'
```

### Night Mode
Add CSS class `night` to body element to enable dark theme:
```html
<body class="night">
```

## License

Please check the license file in the root directory of the repository.

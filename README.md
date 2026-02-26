# Hugo Migration - rukeba.com

## Site Overview
- **Framework**: Hugo v0.157.0 Extended
- **Content**: 225 posts (90 in by-the-way, 135 in songbook)
- **URL**: http://rukeba.com
- **Language**: Russian (ru-RU)

## Local Development

### Requirements
- Hugo Extended v0.157.0 or later
- Git

### Setup
```bash
# Install Hugo (macOS)
brew install hugo

# Install Hugo (Linux)
wget https://github.com/gohugoio/hugo/releases/download/v0.157.0/hugo_extended_0.157.0_linux-amd64.deb
sudo dpkg -i hugo_extended_0.157.0_linux-amd64.deb
```

### Running Locally
```bash
# Start development server
hugo server

# Start with drafts
hugo server -D

# Build for production
hugo --minify
```

Server will be available at http://localhost:1313/

## Project Structure
```
rukeba.github.io/
├── content/
│   ├── by-the-way/        # Blog posts
│   ├── songbook/          # Song lyrics with chords
│   ├── books/             # Book reviews
│   ├── listen/            # Music recommendations
│   └── archive/           # Archive pages
├── themes/
│   └── rukeba/            # Custom theme
│       ├── layouts/       # Templates
│       │   ├── _default/
│       │   ├── by-the-way/
│       │   ├── songbook/
│       │   ├── taxonomy/
│       │   └── partials/
│       └── static/
├── static/                # Static assets
│   ├── assets/           # CSS, JS, images
│   ├── CNAME
│   ├── robots.txt
│   └── favicon.ico
├── hugo.toml             # Hugo configuration
└── .github/
    └── workflows/
        └── hugo.yml      # GitHub Actions deployment
```

## Configuration
Main configuration in `hugo.toml`:
- Base URL: http://rukeba.com
- Language: ru-RU
- Permalinks: `/:section/:slug/`
- RSS feed: `/feed/index.xml`
- Taxonomies: tags and categories
- Google Analytics: UA-1638627-8

## Content
- Blog posts in `content/by-the-way/`
- Songbook in `content/songbook/`
- Front matter uses standard Hugo format with YAML
- Tags for categorization
- Dates in ISO 8601 format

## Deployment
Automated via GitHub Actions:
- Pushes to `main` branch trigger build
- Hugo builds site with `--minify`
- Deploys to GitHub Pages
- Available at http://rukeba.com

## Key Features
- **Two blogs**: by-the-way (blog) and songbook (song lyrics)
- **Tag pages**: Filtered by section (e.g., /by-the-way/tag/ and /songbook/tag/)
- **RSS feeds**: Main feed at /feed/index.xml
- **Redirects**: /blog/ → /by-the-way/, /ra/ → /songbook/
- **SEO**: Meta tags, Open Graph, Twitter Cards
- **Analytics**: Google Analytics UA-1638627-8
- **Responsive**: Bootstrap 3.3.7 styling

## Migration Notes
Migrated from Jekyll to Hugo while preserving:
- All 225 posts with original dates and content
- Exact URL structure for SEO
- Tag functionality per section
- RSS feed location (/feed/index.xml)
- Visual design and styling
- Google Analytics integration
- All static assets and pages

## Maintenance

### Adding Content
```bash
# New blog post
hugo new by-the-way/my-post.md

# New song
hugo new songbook/my-song.md
```

### Updating Theme
Theme files are in `themes/rukeba/layouts/`
- Edit templates as needed
- Changes auto-reload with `hugo server`

### Testing
```bash
# Build and check for errors
hugo

# Check links (if tool available)
hugo --quiet && htmltest public/
```

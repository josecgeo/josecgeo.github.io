---
title: "Installation"
slug: "getting-started/installation"
date: "2025-11-15"
tags: ["setup", "guide"]
menu: true
menu_order: 2
include_in_sitemap: true
draft: false
---

# Installation Guide

## Prerequisites

- A text editor (VS Code, Sublime, etc.)
- A web browser (Chrome, Firefox, Safari, Edge)
- Git (optional, for version control)

## Step 1: Download DocsHub

Clone or download the DocsHub repository:

```bash
git clone https://github.com/josecgeo/docshub.git
cd docshub
```

Or simply extract the downloaded ZIP file to your desired location.

## Step 2: Explore the Directory Structure

```
josecgeo.github.io/
├── index.html              # Main SPA entry point
├── content/
│   ├── config.yaml         # Site configuration
│   ├── theme.yaml          # Theme definitions
│   ├── manifest.yaml       # Page registry
│   ├── getting-started/
│   │   ├── overview.md
│   │   └── installation.md
│   ├── features/
│   │   ├── markdown-support.md
│   │   ├── theming.md
│   │   └── search.md
│   └── api/
│       ├── config.md
│       └── manifest.md
└── assets/                 # Images, icons, etc.
```

## Step 3: Open in Browser

Simply open `index.html` in your web browser:

```
File → Open → index.html
```

Or use a local server:

```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Node.js (with http-server)
npx http-server
```

Then visit: `http://localhost:8000`

## Step 4: Customize Configuration

Edit `content/config.yaml` to set:

- Site name and title
- Default theme
- Footer text and copyright

**Example:**

```yaml
site_name: "My Documentation"
window_title: "My Docs"
slogan: "Learn everything you need"
default_theme: "dark"
footer:
  show_sitemap: true
  copyright: "© 2025 My Company"
```

## Step 5: Add Your First Page

1. Create a new folder under `content/`, e.g., `content/tutorials/`
2. Add a Markdown file: `content/tutorials/getting-started.md`
3. Include frontmatter:

```markdown
---
title: "My First Tutorial"
slug: "tutorials/getting-started"
date: "2025-11-15"
tags: ["tutorial", "beginner"]
menu: true
menu_order: 1
include_in_sitemap: true
draft: false
---

# My First Tutorial

Your content goes here...
```

4. Link it in `content/manifest.yaml`:

```yaml
pages:
  - path: "/tutorials/getting-started.md"
    title: "My First Tutorial"
    slug: "tutorials/getting-started"
    tags: ["tutorial", "beginner"]
    menu_order: 1
    include_in_menu: true
    include_in_sitemap: true
```

5. Reload your browser — the page is now live!

## Troubleshooting

### YAML files not loading
- Check that YAML syntax is valid (use a YAML linter)
- Ensure file paths in manifest.yaml are correct (relative to `content/`)

### Markdown not rendering
- Verify frontmatter is between `---` delimiters
- Check that the file path is linked in manifest.yaml

### Styles not applying
- Clear browser cache (Ctrl+Shift+Delete)
- Check browser console for CSS/JS errors (F12)

## Next Steps

- Learn [Markdown Support](../features/markdown-support)
- Explore [Theming](../features/theming)
- Check the [Configuration Reference](../api/config)

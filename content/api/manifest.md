---
title: "Manifest Schema"
slug: "api/manifest"
date: "2025-11-15"
tags: ["api", "schema"]
menu: true
menu_order: 2
include_in_sitemap: true
draft: false
---

# Manifest Schema Reference

The `content/manifest.yaml` file defines all pages to be displayed on the site. **Only pages listed here will appear.**

## manifest.yaml Structure

```yaml
pages:
  - path: "/path/to/file.md"
    title: "Page Title"
    slug: "category/page-name"
    tags: ["tag1", "tag2"]
    menu_order: 1
    include_in_menu: true
    include_in_sitemap: true
  
  - path: "/another/file.md"
    title: "Another Page"
    slug: "category/another-page"
    tags: ["documentation"]
    menu_order: 2
    include_in_menu: true
    include_in_sitemap: true
```

## Page Entry Fields

### path

**Type:** `string` (file path)  
**Required:** `true`  
**Description:** Relative path to the Markdown file (from `content/` directory).

**Rules:**
- Must start with `/`
- Must point to an existing `.md` file
- Example: `/getting-started/overview.md`

**Example:**
```yaml
path: "/guides/setup.md"
```

### title

**Type:** `string`  
**Required:** `true`  
**Description:** Display title for the page (shown in menu, breadcrumbs, search).

**Rules:**
- Keep under 60 characters for readability
- Use Title Case
- Should match Markdown frontmatter `title`

**Example:**
```yaml
title: "Getting Started with DocsHub"
```

### slug

**Type:** `string` (URL slug)  
**Required:** `true`  
**Description:** URL-friendly identifier for the page.

**Rules:**
- Must be unique across all pages
- Use lowercase with hyphens: `getting-started/overview`
- Should match Markdown frontmatter `slug`
- Defines the URL hash: `#/getting-started/overview`

**Example:**
```yaml
slug: "getting-started/overview"
```

### tags

**Type:** `array` of `string`  
**Required:** `false`  
**Default:** `[]`  
**Description:** Tags for categorization and search filtering.

**Rules:**
- Use lowercase
- Keep tag names short (1–3 words)
- Be consistent (reuse tag names)

**Example:**
```yaml
tags: ["setup", "guide", "beginner"]
```

### menu_order

**Type:** `number`  
**Required:** `false`  
**Default:** `999`  
**Description:** Sort order in the navigation menu (lower values appear first).

**Rules:**
- Use 1–10 for main navigation
- Pages without this field appear at the end
- Applied only if `include_in_menu: true`

**Example:**
```yaml
menu_order: 1
```

### include_in_menu

**Type:** `boolean`  
**Required:** `false`  
**Default:** `true`  
**Description:** Whether the page appears in the sidebar navigation.

**Example:**
```yaml
include_in_menu: true
```

### include_in_sitemap

**Type:** `boolean`  
**Required:** `false`  
**Default:** `true`  
**Description:** Whether the page appears in the footer sitemap.

**Example:**
```yaml
include_in_sitemap: true
```

## Complete Example

```yaml
pages:
  # Getting Started Section
  - path: "/getting-started/overview.md"
    title: "Getting Started"
    slug: "getting-started/overview"
    tags: ["intro", "setup"]
    menu_order: 1
    include_in_menu: true
    include_in_sitemap: true
  
  - path: "/getting-started/installation.md"
    title: "Installation"
    slug: "getting-started/installation"
    tags: ["setup", "guide"]
    menu_order: 2
    include_in_menu: true
    include_in_sitemap: true

  # Features Section
  - path: "/features/markdown.md"
    title: "Markdown Support"
    slug: "features/markdown"
    tags: ["features"]
    menu_order: 1
    include_in_menu: true
    include_in_sitemap: true
  
  - path: "/features/search.md"
    title: "Search"
    slug: "features/search"
    tags: ["features"]
    menu_order: 2
    include_in_menu: true
    include_in_sitemap: true

  # Hidden Page (not in menu or sitemap)
  - path: "/archive/old-docs.md"
    title: "Old Documentation"
    slug: "archive/old-docs"
    tags: ["archive"]
    menu_order: 999
    include_in_menu: false
    include_in_sitemap: false

  # Draft Page (exists but not displayed)
  # Note: Use draft: true in Markdown frontmatter to hide
```

## Adding a New Page

1. **Create the Markdown file:**
   ```bash
   content/
   └── my-section/
       └── my-page.md
   ```

2. **Add frontmatter:**
   ```markdown
   ---
   title: "My Page Title"
   slug: "my-section/my-page"
   date: "2025-11-15"
   tags: ["tag1"]
   menu: true
   menu_order: 1
   include_in_sitemap: true
   draft: false
   ---
   ```

3. **Link in manifest.yaml:**
   ```yaml
   pages:
     - path: "/my-section/my-page.md"
       title: "My Page Title"
       slug: "my-section/my-page"
       tags: ["tag1"]
       menu_order: 1
       include_in_menu: true
       include_in_sitemap: true
   ```

4. **Reload browser** — page appears immediately!

## Menu Grouping

Pages are automatically grouped by their first slug segment:

```yaml
pages:
  - slug: "getting-started/overview"    # → "Getting Started" group
  - slug: "getting-started/install"     # → "Getting Started" group
  - slug: "features/search"             # → "Features" group
  - slug: "features/themes"             # → "Features" group
```

Generates menu:

```
Getting Started
  ├── Overview
  └── Install
Features
  ├── Search
  └── Themes
```

## Validation Checklist

Before deploying, ensure:

- [ ] All `path` values point to existing `.md` files
- [ ] All `slug` values are unique
- [ ] All `slug` values match Markdown frontmatter `slug`
- [ ] All `title` values match or are similar to frontmatter `title`
- [ ] `menu_order` values are in logical order
- [ ] YAML syntax is valid
- [ ] No duplicate entries

## Best Practices

1. **Group related pages** — Use consistent slug prefixes
2. **Consistent naming** — Use title case in titles, lowercase in slugs
3. **Use descriptive titles** — Helps users understand page content
4. **Reuse tags** — Build a consistent tag vocabulary
5. **Order logically** — Use `menu_order` to reflect reading flow
6. **Keep it DRY** — If content appears in multiple places, link rather than duplicate

## Troubleshooting

### Page doesn't appear
- [ ] Check `path` is correct (relative to `content/`)
- [ ] Verify file exists at that path
- [ ] Ensure `include_in_menu: true` (if should appear in menu)

### Page appears but content doesn't load
- [ ] Check Markdown file exists
- [ ] Verify Markdown syntax is valid
- [ ] Check browser console for errors (F12)

### Wrong menu order
- [ ] Verify `menu_order` is a number (not a string)
- [ ] Lower numbers appear first
- [ ] Check pages are in same group (same first slug segment)

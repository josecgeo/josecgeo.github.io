---
title: "Configuration"
slug: "api/config"
date: "2025-11-15"
tags: ["api", "configuration"]
menu: true
menu_order: 1
include_in_sitemap: true
draft: false
---

# Configuration Reference

The `content/config.yaml` file controls global site settings.

## config.yaml Structure

```yaml
site_name: "DocsHub"
window_title: "DocsHub - Documentation Made Simple"
slogan: "Documentation made simple"
favicon: "/assets/favicon.svg"
logo: "/assets/logo.svg"
default_theme: "light"
available_themes:
  - "light"
  - "dark"
  - "blue"
  - "high_contrast"
footer:
  show_sitemap: true
  copyright: "© 2025 DocsHub"
```

## Configuration Fields

### site_name

**Type:** `string`  
**Required:** `true`  
**Description:** The name of your documentation site, displayed in the sidebar header.

**Example:**
```yaml
site_name: "My Product Docs"
```

### window_title

**Type:** `string`  
**Required:** `true`  
**Description:** The title shown in the browser tab and bookmarks.

**Example:**
```yaml
window_title: "My Product - Documentation"
```

### slogan

**Type:** `string`  
**Required:** `false`  
**Description:** A short tagline displayed on the homepage.

**Example:**
```yaml
slogan: "Learn everything in 5 minutes"
```

### favicon

**Type:** `string` (path)  
**Required:** `false`  
**Description:** Path to the favicon file (relative to site root).

**Example:**
```yaml
favicon: "/assets/favicon.svg"
```

### logo

**Type:** `string` (path)  
**Required:** `false`  
**Description:** Path to the logo image (relative to site root).

**Example:**
```yaml
logo: "/assets/logo.png"
```

### default_theme

**Type:** `string`  
**Required:** `false`  
**Default:** `"light"`  
**Description:** The initial theme loaded. Must be in `available_themes`.

**Example:**
```yaml
default_theme: "dark"
```

### available_themes

**Type:** `array` of `string`  
**Required:** `true`  
**Description:** List of theme keys that users can switch between. Themes must be defined in `theme.yaml`.

**Example:**
```yaml
available_themes:
  - "light"
  - "dark"
  - "blue"
  - "my_custom_theme"
```

### footer

**Type:** `object`  
**Required:** `false`  
**Description:** Footer configuration.

#### footer.show_sitemap

**Type:** `boolean`  
**Default:** `true`  
**Description:** Whether to display all pages in the footer sitemap.

#### footer.copyright

**Type:** `string`  
**Default:** `"© 2025"`  
**Description:** Copyright text displayed in the footer.

**Example:**
```yaml
footer:
  show_sitemap: true
  copyright: "© 2025 My Company. All rights reserved."
```

## Complete Example

```yaml
# Site Branding
site_name: "React Documentation"
window_title: "React Docs - Official Documentation"
slogan: "A JavaScript library for building UIs"

# Assets
favicon: "/assets/react.svg"
logo: "/assets/react-logo.png"

# Theme
default_theme: "light"
available_themes:
  - "light"
  - "dark"
  - "high_contrast"

# Footer
footer:
  show_sitemap: true
  copyright: "© 2025 React Team. Licensed under MIT."
```

## Validation

Before deploying, ensure:

- [ ] `site_name` is set
- [ ] `window_title` is set
- [ ] `default_theme` exists in `available_themes`
- [ ] All themes in `available_themes` are defined in `theme.yaml`
- [ ] Asset paths (favicon, logo) are correct (or can be empty strings)
- [ ] YAML syntax is valid

## Loading Configuration

The configuration is loaded automatically on page initialization:

```javascript
async loadConfig() {
  this.config = await this.loadYAML('content/config.yaml');
  document.title = this.config.window_title;
  document.getElementById('site-name').textContent = this.config.site_name;
}
```

## Common Customizations

### Change Site Name

```yaml
site_name: "API Documentation"
window_title: "My API - Developer Documentation"
```

### Set Dark Mode as Default

```yaml
default_theme: "dark"
```

### Add Custom Theme

1. Add to `available_themes`:
```yaml
available_themes:
  - "light"
  - "dark"
  - "my_theme"
```

2. Define in `theme.yaml`:
```yaml
my_theme:
  colors:
    background: "#fafafa"
    text: "#222222"
    sidebar: "#f0f0f0"
    accent: "#007bff"
    border: "#e0e0e0"
  typography:
    font_family: "Georgia, serif"
    base_size: "16px"
```

### Disable Footer Sitemap

```yaml
footer:
  show_sitemap: false
  copyright: "© 2025 My Company"
```

## Performance Tips

- Keep `site_name` under 50 characters
- Use SVG for favicon and logo (smaller file size)
- Limit `available_themes` to 4–5 themes
- Keep copyright text concise

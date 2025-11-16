---
title: "Theming"
slug: "features/theming"
date: "2025-11-15"
tags: ["features", "customization"]
menu: true
menu_order: 2
include_in_sitemap: true
draft: false
---

# Theming System

DocsHub comes with built-in theme support. Users can switch between themes with a single click, and developers can create custom themes easily.

## Built-in Themes

### Light (Default)

Clean, bright theme optimized for daytime reading.

- Background: White (#ffffff)
- Text: Dark gray (#1a1a1a)
- Accent: Bright blue (#0070f3)

### Dark

Easy on the eyes for low-light environments.

- Background: Near black (#111111)
- Text: Light gray (#eeeeee)
- Accent: Sky blue (#4dabf7)

### Blue

Professional blue theme for corporate documentation.

- Background: Light blue (#f0f4ff)
- Text: Dark blue (#0a0e27)
- Accent: Navy (#0051ba)

### High Contrast

Accessibility-focused theme with maximum contrast.

- Background: White (#ffffff)
- Text: Pure black (#000000)
- Accent: Pure black (#000000)

## Customizing Themes

Edit `content/theme.yaml` to modify colors and typography:

```yaml
light:
  colors:
    background: "#ffffff"
    text: "#1a1a1a"
    sidebar: "#f5f5f5"
    accent: "#0070f3"
    border: "#e5e5e5"
  typography:
    font_family: "Inter, system-ui, sans-serif"
    base_size: "16px"

dark:
  colors:
    background: "#111111"
    text: "#eeeeee"
    sidebar: "#1d1d1d"
    accent: "#4dabf7"
    border: "#333333"
  typography:
    font_family: "Inter, system-ui, sans-serif"
    base_size: "16px"
```

## Creating a New Theme

1. Add a new theme block in `theme.yaml`:

```yaml
my_theme:
  colors:
    background: "#f9f9f9"
    text: "#333333"
    sidebar: "#eeeeee"
    accent: "#ff6b6b"
    border: "#dddddd"
  typography:
    font_family: "Georgia, serif"
    base_size: "16px"
```

2. Add it to `config.yaml`:

```yaml
available_themes:
  - "light"
  - "dark"
  - "my_theme"
```

3. Reload the page — your new theme appears in the theme switcher!

## Color Variables

Each theme uses these CSS variables:

| Variable | Usage |
|----------|-------|
| `--bg` | Page background |
| `--text` | Primary text color |
| `--sidebar` | Sidebar background |
| `--accent` | Links, buttons, highlights |
| `--border` | Divider lines |

## Accessibility Guidelines

When creating themes, ensure:

- **Contrast Ratio**: Text contrast ≥ 4.5:1 (WCAG AA)
- **Large Text**: Large text ≥ 3:1 contrast
- **Color Independence**: Don't rely solely on color (use icons/labels too)
- **Focus Indicators**: Always visible keyboard focus (default browser focus is fine)

## System Preference Detection

DocsHub respects the user's system theme preference:

```javascript
const isDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
```

If no saved theme preference, the site loads the user's system theme.

## Saving Theme Preference

User theme selection is saved to browser localStorage:

```javascript
localStorage.setItem('theme', 'dark');
```

This persists across browser sessions.

## Performance

- Theme colors are applied via CSS variables (instant switching)
- No page reload needed
- Smooth transitions between themes

## Testing Your Theme

1. Open the site
2. Click the theme toggle (🌙 button)
3. Verify all colors look good
4. Check readability at different font sizes
5. Test with accessibility tools (Lighthouse, axe DevTools)

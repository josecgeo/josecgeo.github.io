# Navigation System Guide

## Overview

The documentation site now supports a powerful, flexible navigation system with the following features:

### Key Features

1. **Dynamic Content Discovery**: Automatically discovers content structure from the `content/` directory
2. **8-Level Deep Navigation**: Supports up to 8 levels of nested folders for complex documentation structures
3. **Horizontal Top Menu**: First-level pages appear as a horizontal menu bar
4. **Menu Configuration via Frontmatter**: Control menu position, title, and visibility through markdown frontmatter
5. **Smart Search**: Search is only visible when sidebar/navigation is active (desktop) or hamburger menu is open (mobile)
6. **Responsive Design**: Optimized for all screen sizes

## Menu Configuration

### Frontmatter Options

Add frontmatter to any first-level `index.md` file to configure its appearance in the horizontal menu:

```markdown
---
menu_position: 1
menu_title: Home
menu_hidden: false
---

# Your Page Title
```

#### Available Options

- **`menu_position`**: Number (default: 999) - Controls the order in the horizontal menu. Lower numbers appear first.
- **`menu_title`**: String (default: folder name) - Custom title to display in the menu instead of the folder name
- **`menu_hidden`**: Boolean (default: false) - Set to `true` to hide this page from the horizontal menu

### Examples

#### Example 1: Set Menu Order
```markdown
---
menu_position: 1
menu_title: Home
---
```

#### Example 2: Hide from Menu
```markdown
---
menu_hidden: true
---
```

#### Example 3: Custom Title
```markdown
---
menu_position: 2
menu_title: API Reference
---
```

## Search Functionality

### Search Visibility

The search box is now located in the header and is:
- **Visible on desktop** when navigation content exists
- **Hidden on mobile** by default (to save space)
- **Smart**: Automatically shows/hides based on whether there's content to search

### Search Shortcuts

- Press `Ctrl+K` (or `Cmd+K` on Mac) to focus the search box
- Press `Escape` to close search results

## Navigation Structure

### Folder Organization

```
content/
├── home/
│   └── index.md          (menu_position: 1)
├── docs/
│   ├── index.md          (menu_position: 2)
│   ├── installation.md
│   └── usage.md
├── about/
│   ├── index.md          (menu_position: 3)
│   └── team.md
└── blog/
    ├── index.md          (menu_position: 4)
    ├── first-post.md
    └── second-post.md
```

### Horizontal Menu Display

With the above configuration, the horizontal menu will show:
```
[Home] [Documentation] [About] [Blog]
```

### Deep Nesting Support

The system supports up to 8 levels of nesting:

```
content/
├── level1/
│   ├── index.md
│   └── level2/
│       ├── index.md
│       └── level3/
│           ├── index.md
│           └── ... (up to level8)
```

## Layout Files

### Footer & Header Rendering

Both `_header.md` and `_footer.md` now properly render markdown:

- **`_header.md`**: Controls the header subtitle (if no tagline is set in `_config.md`)
- **`_footer.md`**: Fully rendered markdown for footer content, including links and formatting

Example `_footer.md`:
```markdown
© 2025 DocsHub. All rights reserved.

Built with ❤️ using HTML + CSS + JavaScript.

[GitHub](https://github.com/josecgeo) | [Contact](mailto:contact@example.com)
```

## CSS Customization

### Menu Positioning

The navigation bar uses CSS flexbox with order control:

```css
#breadcrumb-wrap {
  order: 1;  /* Left side */
}

.top-menu {
  order: 2;  /* Center */
}
```

### Responsive Behavior

On mobile (≤768px):
- Top menu moves to full width, order 1
- Breadcrumbs move to full width, order 2
- Search is hidden to save space

## Best Practices

1. **Always include `index.md`** in first-level folders that should appear in the horizontal menu
2. **Use menu_position** to control order (1, 2, 3, etc.)
3. **Keep menu titles short** for better mobile display
4. **Hide internal sections** using `menu_hidden: true` for sections you don't want in the top menu
5. **Test on mobile** to ensure navigation is clear and accessible

## Troubleshooting

### Menu not showing
- Ensure `index.md` exists in the folder
- Check that `menu_hidden` is not set to `true`
- Verify folder is listed in the content discovery system

### Search not visible
- Search only shows when there's content to search
- On mobile, search is hidden by default (design decision for cleaner UI)
- Toggle sidebar to check if content structure is properly loaded

### Footer/Header not rendering markdown
- Ensure `_footer.md` and `_header.md` are in the `content/` directory
- Check browser console for any loading errors
- Verify markdown syntax is correct

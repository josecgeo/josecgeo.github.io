---
type: "site_structure"
description: "Defines the site navigation, menus, and page organization"
---

# Site Manifest & Navigation

This file describes what pages exist and how they appear in menus and search results.

## Site Structure

```yaml
sections:
  home:
    pages:
      - index
    visible_in_menu: true
    searchable: true
  
  about:
    pages:
      - index
      - team
    visible_in_menu: true
    searchable: true
  
  blog:
    pages:
      - index
      - first-post
      - second-post
    visible_in_menu: true
    searchable: true
  
  docs:
    pages:
      - index
      - installation
      - usage
    visible_in_menu: true
    searchable: true
```

## Menu Configuration

Each section can be customized by editing its `index.md` file frontmatter:

```yaml
menu_settings:
  position: "Number to determine order (1 = first, 2 = second, etc.)"
  title: "Custom name to show in menu (defaults to section name)"
  hidden: "true/false - hide this section from menu if needed"
  icon: "Emoji or icon to display next to the name"
```

## Page Discoverability

### What Gets Searched?
- Page titles
- Page content
- File names

### What Gets Shown in Navigation?
- Sections with `menu_hidden: false`
- Pages listed in this manifest

### What Gets Included in Sitemap?
- All pages marked as `searchable: true`

## Adding New Pages

To add a new page:

1. Create a `.md` file in the appropriate section folder
2. Add the filename to this manifest under that section's `pages` list
3. The page will automatically appear in search results and menus
4. No code changes needed!

## Example: Adding a New Section

1. Create a new folder in `content/` (e.g., `tutorials/`)
2. Add an `index.md` file to that folder
3. Add the section to this manifest with its pages
4. Refresh your browser

The new section will appear in the menu automatically.

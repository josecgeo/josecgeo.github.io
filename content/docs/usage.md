# Usage Guide

Learn how to use and customize your documentation site.

## Adding New Pages

### 1. Create Markdown File

Create a new `.md` file in the appropriate directory:

```bash
content/docs/new-page.md
```

### 2. Update Content Structure

In `index.html`, update the `CONTENT_STRUCTURE` object:

```javascript
const CONTENT_STRUCTURE = {
  docs: ['index', 'installation', 'usage', 'new-page']
};
```

### 3. Add Content

Write your content in Markdown:

```markdown
# New Page Title

Your content here with **bold** and *italic* text.

## Section

More content...
```

## Customizing the Site

### Site Name and Tagline

Edit `content/_config.md`:

```markdown
---
site_name: Your Site Name
tagline: Your Tagline Here
---
```

### Logo

Replace `content/logo.svg` with your own SVG logo.

### Header and Footer

- Edit `content/_header.md` for header content
- Edit `content/_footer.md` for footer content

## Markdown Features

The site supports standard Markdown:

- **Bold text**
- *Italic text*
- `Code blocks`
- [Links](https://example.com)
- Lists (ordered and unordered)
- Tables
- Blockquotes

## Styling

The site uses CSS variables for easy theming. Edit the `:root` styles in `index.html` to customize colors and spacing.

## Search

The search functionality automatically indexes all markdown content. No additional configuration needed!

---

*Last updated: January 2025*

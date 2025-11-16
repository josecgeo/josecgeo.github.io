---
title: "Markdown Support"
slug: "features/markdown-support"
date: "2025-11-15"
tags: ["features", "markdown"]
menu: true
menu_order: 1
include_in_sitemap: true
draft: false
---

# Markdown Support

DocsHub uses [marked.js](https://marked.js.org/) to render Markdown into HTML. All standard Markdown syntax is supported, plus additional features for richer documentation.

## Basic Syntax

### Headings

```markdown
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```

### Emphasis

```markdown
*Italic* or _italic_
**Bold** or __bold__
***Bold and italic***
~~Strikethrough~~
```

### Lists

**Unordered:**

```markdown
- Item 1
- Item 2
  - Nested item
  - Another nested item
- Item 3
```

**Ordered:**

```markdown
1. First
2. Second
3. Third
```

### Links

```markdown
[Link text](https://example.com)
[Internal page](/getting-started/overview)
```

### Images

```markdown
![Alt text](/assets/image.png)
```

### Code

**Inline code:**

```markdown
This is `inline code` in a sentence.
```

**Code blocks:**

````markdown
```javascript
function hello() {
  console.log('Hello, DocsHub!');
}
```

```python
def hello():
    print("Hello, DocsHub!")
```

```yaml
config:
  site_name: "My Site"
  theme: "dark"
```
````

## Advanced Formatting

### Blockquotes

```markdown
> This is a blockquote
> 
> It can span multiple lines
> 
> > And can be nested
```

### Tables

```markdown
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Data 1   | Data 2   | Data 3   |
| Data 4   | Data 5   | Data 6   |
```

### Horizontal Rules

```markdown
---
or
***
or
___
```

## Frontmatter

Every Markdown file can have frontmatter metadata at the top:

```markdown
---
title: "Page Title"
slug: "path/to/page"
date: "2025-11-15"
tags: ["tag1", "tag2"]
menu: true
menu_order: 1
include_in_sitemap: true
draft: false
---

# Your content here
```

### Frontmatter Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| title | string | Yes | Page title |
| slug | string | Yes | URL-friendly identifier |
| date | ISO 8601 | No | Publication date |
| tags | array | No | Categorization tags |
| menu | boolean | No | Show in menu (default: true) |
| menu_order | number | No | Sort order |
| include_in_sitemap | boolean | No | Show in footer sitemap (default: true) |
| draft | boolean | No | Hide if true (default: false) |

## Best Practices

1. **Use descriptive headings** — Helps with SEO and accessibility
2. **Break content into sections** — Use multiple headings
3. **Use code blocks** — Syntax highlighting for clarity
4. **Add links** — Connect related pages
5. **Keep lines short** — Easier to read and maintain
6. **Use lists** — Break down complex information

## HTML Sanitization

All rendered HTML is sanitized using [DOMPurify](https://github.com/cure53/DOMPurify) to prevent XSS attacks. This means:

- ✅ Standard HTML tags are safe: `<strong>`, `<em>`, `<a>`, etc.
- ✅ Markdown links work correctly
- ✅ Code blocks are preserved
- ❌ Inline scripts (`<script>`) are removed
- ❌ Event handlers (`onclick`, etc.) are removed

## Performance Note

For best performance with many pages:

- Keep Markdown files under 50 KB
- Use headings to break up long content
- Minimize the number of images
- Use relative links for internal navigation

# DocsHub - Business Logic & User Guide

This document explains how DocsHub works from a business perspective, not the technical implementation.

---

## What is DocsHub?

DocsHub is a professional documentation and content management system. It's designed to make it easy for anyone to create, organize, and publish documentation without requiring technical knowledge.

**Key Benefits:**
- No server or database needed
- All content is stored as simple text files
- Automatically creates a professional-looking website
- Works on any device - desktop, tablet, or mobile
- Light and dark mode options
- Powerful search functionality

---

## How Content is Organized

### Sections
Your content is organized into **sections** (like folders). Each section contains multiple pages.

**Default Sections:**
- **Home** - Your main landing page
- **About** - Team and project information
- **Blog** - Articles and news posts
- **Docs** - Technical documentation and guides

### Pages
Each section contains one or more **pages**. For example:
- Home section has: Home Page
- Blog section has: Blog Index, First Post, Second Post
- Docs section has: Installation Guide, Usage Guide

### Navigation
- **Top Menu** - Shows main sections (Home, About, Blog, Docs)
- **Sidebar** - Shows all pages within each section
- **Breadcrumbs** - Shows your current location (e.g., Docs > Installation)
- **Search** - Find any content instantly

---

## Managing Your Content

### Adding a New Page

**Step 1:** Create a text file (`.md` format) in the appropriate section folder
**Step 2:** Write your content using simple Markdown formatting
**Step 3:** Update `manifest.md` to list your new page
**Step 4:** Refresh your browser - that's it!

Example: To add a new blog post
1. Create file: `content/blog/my-new-post.md`
2. Write your content
3. Add to `manifest.md` under blog section
4. Your post appears in the blog menu

### Creating a New Section

**Step 1:** Create a new folder in `content/`
**Step 2:** Add an `index.md` file to that folder
**Step 3:** Add the section to `manifest.md`
**Step 4:** Customize the menu position and title in `index.md`

### Menu Customization

In any section's `index.md` file, you can control:
- **Menu Position** - Which order sections appear (1 = first, 2 = second)
- **Menu Title** - What text shows in the menu
- **Hidden** - Whether to hide this section from the menu

Example `index.md` frontmatter:
```
---
menu_position: 2
menu_title: Articles
menu_hidden: false
---
```

---

## Configuration Files

### `_config.md` - Site Settings
Controls overall site appearance and branding:
- **Site Name** - Displayed in header (e.g., "DocsHub")
- **Tagline** - Subtitle next to site name
- **Window Title** - Text shown in browser tab

### `theme.md` - Colors & Appearance
Define colors for light and dark modes:
- Background colors
- Text colors
- Link/accent colors
- Button colors

Make changes and see them live immediately!

### `manifest.md` - Navigation Structure
Defines what sections and pages exist on your site:
- Which pages are searchable
- Which pages appear in menus
- Section organization

### `_header.md` - Header Content
Custom content displayed at the top (optional)

### `_footer.md` - Footer Content
Copyright info, links, and other footer content

### `favicon.svg` - Site Icon
The small icon shown in the browser tab

### `logo.svg` - Site Logo
Your company/project logo displayed in the header

---

## Content Features

### Markdown Formatting

Write your pages using **Markdown** - a simple, readable text format:

```
# Main Heading
## Subheading
### Sub-subheading

**Bold text**
*Italic text*

- Bullet list
- Another item

1. Numbered list
2. Another item

[Link text](https://example.com)

> Quote or note
```

### Page Metadata (Frontmatter)

At the top of each page, you can add metadata:

```
---
menu_position: 1
menu_title: Home
menu_hidden: false
---

# Page Content Starts Here
```

---

## Search & Discovery

### How Search Works
- Searches page titles and content
- Real-time results as you type
- Shows preview of matching content
- Click to navigate to page

### Keyboard Shortcuts
- **Ctrl+K** (or **Cmd+K** on Mac) - Focus search
- **Escape** - Close search results

### What Gets Indexed
- All pages marked as searchable in `manifest.md`
- Page titles and content
- File names

---

## Visual Appearance

### Responsive Design
- **Desktop** - Full sidebar navigation
- **Tablet** - Sidebar in dropdown drawer
- **Mobile** - Touch-friendly layout
- **Small Mobile** - Minimal spacing, optimized for small screens

### Dark Mode
- Toggle button in top right
- Remembers your preference
- All colors automatically adjusted

### Theme Customization
Edit `theme.md` to change colors:
1. Find the color you want to change
2. Replace the hex color value
3. Save the file
4. Refresh your browser

Example: Change accent color from blue to green
```yaml
accent_color: "#22c55e"  # Changed from #3b82f6
```

---

## Site Structure

```
content/
├── favicon.svg         # Browser tab icon
├── logo.svg            # Header logo
├── _config.md          # Site configuration
├── _header.md          # Header content
├── _footer.md          # Footer content
├── theme.md            # Colors and appearance
├── manifest.md         # Navigation and structure
├── home/               # Home section
│   └── index.md
├── about/              # About section
│   ├── index.md
│   └── team.md
├── blog/               # Blog section
│   ├── index.md
│   ├── first-post.md
│   └── second-post.md
└── docs/               # Documentation section
    ├── index.md
    ├── installation.md
    └── usage.md
```

---

## Common Tasks

### Update Site Name
Edit `_config.md`:
```yaml
site_name: "My New Company Name"
```

### Add a New Blog Post
1. Create: `content/blog/post-title.md`
2. Add to `manifest.md` under blog pages
3. Refresh browser

### Change Color Scheme
Edit `theme.md`:
- Light mode colors for daytime use
- Dark mode colors for nighttime use

### Hide a Section from Menu
In that section's `index.md`:
```yaml
menu_hidden: true
```

### Reorder Menu Items
Change `menu_position` numbers:
- Lower numbers appear first
- 1, 2, 3... = first, second, third, etc.

### Update Footer
Edit `_footer.md` with your copyright and contact info

---

## Best Practices

✅ **Do:**
- Use descriptive page titles
- Organize related content in sections
- Update the manifest when adding pages
- Keep file names lowercase and simple
- Use clear, concise writing

❌ **Don't:**
- Use special characters in file names
- Leave pages unorganized
- Forget to update manifest.md
- Use complicated folder structures
- Mix content types in one section

---

## Frequently Asked Questions

**Q: Do I need to rebuild the site after making changes?**
A: No! Just refresh your browser. Changes are reflected immediately.

**Q: What if I accidentally delete a page?**
A: It will show a 404 error. Add the file back and refresh.

**Q: Can I have more than 4 sections?**
A: Yes! Create a new folder in `content/` and add it to `manifest.md`.

**Q: Is there a limit to how many pages I can have?**
A: No, you can have as many pages and sections as you need.

**Q: How do I change fonts?**
A: Font changes require editing the HTML file (technical change).

**Q: Can I schedule content to publish at a specific time?**
A: Not built-in, but you can manually add/remove pages as needed.

**Q: How do I add images?**
A: Host them externally and link in Markdown: `![alt text](https://example.com/image.jpg)`

**Q: Can multiple people edit content?**
A: Yes, with version control (Git), people can collaborate on content.

---

## Support & Troubleshooting

**Page Not Showing in Menu?**
- Check if it's in `manifest.md`
- Verify `menu_hidden` is not set to true
- Check spelling of file names

**Colors Not Changing?**
- Edit `theme.md` and save
- Hard-refresh your browser (Ctrl+Shift+R)
- Check hex color format is valid

**Search Not Finding My Content?**
- Verify page is in `manifest.md`
- Check `searchable: true` setting
- Wait a moment for index to load

**Mobile Menu Not Working?**
- Try refreshing the page
- Clear browser cache
- Try a different browser

---

**Version**: 1.0  
**Last Updated**: November 2025  
**For**: DocsHub Users

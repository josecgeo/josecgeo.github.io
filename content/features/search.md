---
title: "Full-Text Search"
slug: "features/search"
date: "2025-11-15"
tags: ["features", "search"]
menu: true
menu_order: 3
include_in_sitemap: true
draft: false
---

# Full-Text Search

DocsHub includes a fast, client-side full-text search engine built directly into the browser.

## How Search Works

1. **Index Building**: When the page loads, DocsHub scans `manifest.yaml` and builds a search index
2. **Typing**: As users type in the search box, results update instantly
3. **Filtering**: Results are filtered by page titles and tags
4. **Navigation**: Click a result to navigate to that page

## Using Search

1. Click the **search box** in the header or press `Ctrl+K`
2. **Type** your query (minimum 2 characters)
3. **See results** appear instantly below
4. **Click** a result or press **Enter** to navigate

### Keyboard Shortcuts

- `Ctrl+K` — Focus search box (on supported browsers)
- `Escape` — Close search results
- `Arrow Keys` — Navigate results (future enhancement)
- `Enter` — Navigate to selected result

## Search Features

### Title Matching

Search looks for matches in page titles:

```
Query: "config"
Results: 
  ✓ Configuration
  ✓ Advanced Settings
```

### Tag Matching

Search also matches against page tags:

```
Query: "setup"
Results:
  ✓ Getting Started (tags: intro, setup)
  ✓ Installation (tags: setup, guide)
```

### Multiple Results

Top 5 results are shown, sorted by relevance:

```
Query: "theme"
Results:
  1. Theming (title match)
  2. Getting Started (tag match: "customization")
  3. Configuration (tag match: "configuration")
```

## Search Index Structure

The search index is built from manifest entries:

```javascript
{
  slug: "features/search",
  title: "Full-Text Search",
  tags: ["features", "search"],
  text: "Full-Text Search features search"
}
```

## Performance

- **Index Size**: Minimal (~1 KB per page)
- **Search Speed**: < 100 ms for typical sites
- **Memory**: Negligible impact on browser
- **No Backend**: Entirely client-side

## Limitations

Currently, search searches:
- ✅ Page titles
- ✅ Page tags
- ❌ Page content (not yet implemented)

Future versions may add:
- Full content search
- Fuzzy matching (typo tolerance)
- Advanced filters
- Search history

## Customizing Search

To modify search behavior, edit the `setupSearch()` method in `index.html`:

```javascript
setupSearch() {
  const searchBox = document.getElementById('search');
  const resultsDiv = document.getElementById('search-results');

  searchBox.addEventListener('input', (e) => {
    const query = e.target.value.toLowerCase();

    if (query.length < 2) {
      resultsDiv.classList.remove('open');
      return;
    }

    const results = this.searchIndex
      .filter(item => item.text.toLowerCase().includes(query))
      .slice(0, 5);  // <-- Change result count here

    // Render results...
  });
}
```

## Best Practices

1. **Use descriptive titles** — Makes search more useful
2. **Add relevant tags** — Improves discoverability
3. **Keep tag names consistent** — Use standard terminology
4. **Test search** — Verify your site is searchable

## Accessibility

- Search box is keyboard accessible
- Results list is properly marked up
- Screen readers can navigate results
- Focus indicators are visible

# DocsHub Logic Documentation

This document describes the complete logic and architecture of the DocsHub static site generator in a human-readable YAML format for AI and human understanding.

## System Overview

```yaml
system:
  name: "DocsHub - Markdown-Powered Single Page Application (SPA)"
  type: "Static Site Generator"
  technology_stack:
    - "HTML5"
    - "CSS3 (with CSS Variables for theming)"
    - "Vanilla JavaScript"
    - "Markdown (via marked.js library)"
  purpose: "Convert markdown files from a content directory into a professional, responsive documentation website"
  target_users: ["Technical writers", "Documentation teams", "Project maintainers"]

core_principles:
  - "No build process required"
  - "All content in markdown files"
  - "Configuration via YAML frontmatter"
  - "Fully responsive and accessible"
  - "Dark mode support with theme customization"
  - "Full-text search capability"
  - "Client-side routing with hash-based URLs"
```

## Project Structure

```yaml
project_structure:
  root_files:
    - "index.html": "Main SPA entry point with all HTML, CSS, and JavaScript"
    - "logic.md": "This documentation file"
  
  content_directory: "content/"
    structure:
      "favicon.svg": "Website favicon (32x32 SVG)"
      "_config.md": 
        description: "Site configuration with frontmatter"
        frontmatter_keys:
          - "site_name": "Name displayed in header"
          - "tagline": "Subtitle displayed next to site name"
          - "window_title": "Title shown in browser tab (optional)"
      
      "_header.md":
        description: "Optional header content (not currently displayed, but loaded)"
        usage: "Can be extended for custom header content"
      
      "_footer.md":
        description: "Footer content displayed at bottom of every page"
        format: "Markdown (converted to HTML)"
      
      "theme.json":
        description: "Color theme configuration"
        structure:
          light:
            bg, card, text, accent, borders, shadows, etc.
          dark:
            bg, card, text, accent, borders, shadows, etc.
      
      "logo.svg":
        description: "Site logo displayed in header (optional)"
      
      "folders/":
        pattern: "One folder per main section"
        examples: ["home/", "about/", "blog/", "docs/"]
        contents:
          - "index.md": "Overview page for the section (appears in top menu and sidebar)"
          - "other-files.md": "Additional pages in the section"
```

## Content Structure

```yaml
content_organization:
  dynamic_discovery:
    method: "Attempts to load content/.manifest.json for dynamic discovery"
    fallback: "Uses pre-tested fallback structure if manifest unavailable"
    benefits:
      - "Supports up to 8 levels of nested folders"
      - "No rebuild needed when adding new content"
      - "Graceful degradation if discovery fails"
    manifest_format: "JSON file mapping folders to file arrays"
    example_manifest: |
      {
        "home": ["index"],
        "docs": ["index", "installation", "usage"],
        "blog": ["index", "first-post", "second-post"]
      }
  
  folder_system:
    structure: "Up to 8 levels of nested folders supported"
    first_level_folders:
      display_in: "Horizontal top menu"
      linked_by: "Folder index.md file"
      icon_mapping:
        home: "🏠"
        about: "ℹ️"
        blog: "📝"
        docs: "📚"
      default_icon: "📁"
    
    subfolder_files:
      display_in: "Sidebar (expandable/collapsible)"
      structure: "Nested under parent folder"
  
  frontmatter_config:
    location: "At top of .md files between --- delimiters"
    parsing: "YAML format (key: value pairs)"
    first_level_index_pages:
      - "menu_position": "Integer for sorting in top menu (lower numbers first)"
      - "menu_title": "Custom title for top menu link (defaults to folder name)"
      - "menu_hidden": "true/false to hide from menu"
    
    examples:
      home_index: |
        ---
        menu_position: 1
        menu_title: Home
        ---
      blog_index: |
        ---
        menu_position: 2
        menu_title: Articles
        menu_hidden: false
        ---
```

## Rendering Pipeline

```yaml
page_load_sequence:
  1_initialization:
    - "Parse frontmatter from _config.md"
    - "Load theme colors from theme.json"
    - "Load and display logo.svg if present"
    - "Build sidebar navigation structure"
    - "Build top horizontal menu"
    - "Set initial page title from config"
  
  2_route_handling:
    url_format: "#/folder/filename (hash-based routing)"
    default_route: "#/home/index"
    resolution_process:
      1: "Extract folder and filename from URL hash"
      2: "Verify folder exists in CONTENT_STRUCTURE"
      3: "Verify filename exists in folder"
      4: "Load markdown file via fetch()"
      5: "Cache content for performance"
      6: "Show 404 if not found"
  
  3_content_rendering:
    steps:
      1: "Fetch markdown file from content/{folder}/{file}.md"
      2: "Check CONTENT_CACHE to avoid re-fetching"
      3: "Parse with marked.js library"
      4: "Apply markdown rendering with GitHub Flavored Markdown (GFM)"
      5: "Insert rendered HTML into #content card"
      6: "Generate breadcrumb navigation"
      7: "Update sidebar active state"
      8: "Update top menu active state"
      9: "Scroll to top smoothly"
```

## Navigation System

```yaml
navigation_components:
  
  1_header:
    location: "Top sticky bar"
    elements:
      - hamburger_menu_button: "Toggles sidebar on mobile"
      - logo_and_title: "Site name with gradient effect"
      - search_bar: "Full-text search (desktop only)"
      - theme_toggle: "Switch between light/dark mode"
  
  2_top_menu:
    behavior: "Horizontal navigation bar below header"
    contents: "First-level folder links from content/"
    sorting: "By menu_position frontmatter in index.md"
    visibility: "Hidden from top menu if menu_hidden: true"
    responsive: "Wraps on smaller screens"
  
  3_sidebar:
    behavior: "Collapsible folder tree (hidden on mobile, overlay on medium screens)"
    structure:
      - "Folder headers (clickable to index.md)"
      - "Expandable/collapsible file lists per folder"
      - "File links within each folder"
    mobile_behavior:
      - "Fixed overlay triggered by hamburger button"
      - "Close button in top right"
      - "Semi-transparent backdrop"
      - "Closes automatically when link clicked"
    desktop_behavior:
      - "Sticky positioned beside main content"
      - "Scrollable if content exceeds viewport"
  
  4_breadcrumbs:
    display_condition: "Only on non-index pages"
    format: "Folder / File path"
    links: "Clickable back navigation"
    styling: "Small pill-shaped elements with hover effects"

  5_search:
    locations: 
      - "Header (desktop > 768px)"
      - "Sidebar (mobile on-demand)"
    functionality:
      - "Real-time full-text search"
      - "Searches filename + content"
      - "Shows excerpt of matching text"
      - "Results clickable to jump to page"
      - "Debounced (200ms) for performance"
    keyboard_shortcuts:
      - "Ctrl/Cmd + K: Focus search"
      - "Escape: Close search results"
```

## Search Implementation

```yaml
search_system:
  trigger:
    keyboard: "Real-time input event listener"
    debounce_delay: "200ms to avoid excessive processing"
  
  search_scope:
    searches: "Filename + entire markdown content"
    case_sensitivity: "Case-insensitive (converted to lowercase)"
    pattern_matching: "Simple substring matching"
  
  results_display:
    format:
      title: "Folder / Filename"
      excerpt: "120 character snippet around match (60 chars before/after)"
      context: "Ellipsis (...) added if truncated"
    sorting: "Order found during content iteration"
    max_visible: "Scrollable dropdown (400px max-height)"
    empty_state: "Shows 'No results found' message"
  
  interaction:
    click: "Navigate to matching page"
    keyboard: "Enter on focused result"
    close: "Click outside, press Escape, or click on result"
```

## Theming System

```yaml
theme_management:
  
  light_mode:
    default: true
    colors_affected:
      - "Background (--bg)"
      - "Cards (--card)"
      - "Text (--text, --text-secondary)"
      - "Accents (--accent, --accent-hover)"
      - "Navigation (--nav)"
      - "Borders (--border, --border-light)"
      - "Shadows (--shadow, --shadow-md, --shadow-lg)"
  
  dark_mode:
    trigger: "Click theme toggle button"
    css_mechanism: "[data-theme='dark'] attribute on html element"
    storage: "Persisted in localStorage as 'spa-theme'"
    icon_change: "🌙 (dark) ↔ ☀️ (light)"
  
  custom_theme_colors:
    source: "content/theme.json"
    structure:
      light:
        "--bg": "#fafbfc"
        "--card": "#ffffff"
        "--text": "#111827"
        "--accent": "#3b82f6"
        # ... etc
      dark:
        "--bg": "#0f172a"
        "--card": "#1e293b"
        "--text": "#f1f5f9"
        "--accent": "#60a5fa"
        # ... etc
    application:
      method: "CSS custom properties via root.style.setProperty()"
      timing: "Applied on theme toggle"
      fallback: "Uses default CSS variables if theme.json not found"
```

## Responsive Design

```yaml
responsive_breakpoints:
  
  desktop:
    width: "> 1024px"
    layout: "Two-column (sidebar + content)"
    sidebar: "Sticky, always visible"
    search: "Visible in header"
    menu: "All items visible"
  
  tablet:
    width: "768px - 1024px"
    layout: "Single column with drawer sidebar"
    sidebar: "Fixed overlay (hidden by default, toggle shows)"
    search: "Hidden from header, available in sidebar"
    menu: "Wrapped, full-width navigation"
  
  mobile:
    width: "< 768px"
    layout: "Single column"
    sidebar: "Full-height overlay with semi-transparent backdrop"
    search: "Only in sidebar when open"
    header: "Reduced padding and font sizes"
    content: "Reduced padding"
    menu: "Stacked, reduced font size"
  
  small_mobile:
    width: "< 480px"
    header: "Minimal spacing, smaller icons (24px)"
    buttons: "Smaller padding and font"
    breadcrumbs: "Reduced font size (0.75rem)"
    spacing: "Aggressive padding reduction throughout"
```

## Caching Strategy

```yaml
content_caching:
  mechanism: "CONTENT_CACHE object in JavaScript"
  key_format: "folder/filename"
  populate_on: "First request to fetch markdown file"
  benefit: "Eliminates duplicate network requests"
  ttl: "Session-based (cleared on page refresh)"
  scope: "Prevents re-fetching of already loaded content"
```

## Event Handling

```yaml
event_listeners:
  
  navigation:
    - "hashchange: Triggered when URL hash changes"
    - "click on sidebar links: Navigate and close sidebar (mobile)"
    - "click on menu links: Update active states"
  
  ui_interactions:
    - "toggle-sidebar button: Show/hide sidebar"
    - "toggle-theme button: Switch light/dark mode"
    - "Escape key: Close sidebar on mobile"
    - "Ctrl/Cmd + K: Focus search input"
  
  responsive:
    - "resize: Rebuild navigation on breakpoint change"
      debounce: "250ms to prevent excessive recalculation"
      actions:
        - "Close sidebar on desktop transition"
        - "Rebuild sidebar structure"
        - "Update menu styles"
  
  search:
    - "input event: Debounced search execution"
    - "click outside: Close results"
    - "click result: Navigate and close"
```

## Performance Optimizations

```yaml
optimizations:
  
  caching:
    - "Content cached after first fetch"
    - "Theme colors cached in memory"
    - "Menu config cached after load"
  
  rendering:
    - "CSS animations use GPU acceleration (transform, opacity)"
    - "Debounced search (200ms) and resize (250ms)"
    - "Smooth scroll behavior for navigation"
  
  critical_rendering_path:
    1: "Load HTML (inline CSS and JS)"
    2: "Load Google Fonts"
    3: "Load marked.js from CDN"
    4: "Execute initialization"
    5: "Fetch content on first route"
```

## Accessibility Features

```yaml
accessibility:
  
  semantic_html:
    - "Proper heading hierarchy (h1 > h2 > h3, etc.)"
    - "Semantic tags: <header>, <nav>, <main>, <footer>, <aside>"
    - "Links have descriptive text"
  
  aria_attributes:
    - "aria-label on icon buttons"
    - "role attributes where needed"
    - "aria-current for active navigation"
  
  keyboard_navigation:
    - "Tab through interactive elements"
    - "Enter/Space to activate buttons"
    - "Escape to close modals/overlays"
    - "Ctrl/Cmd + K to focus search"
  
  visual_accessibility:
    - "Color contrast meets WCAG AA standards"
    - "Focus states clearly visible"
    - "Sufficient spacing between touch targets (minimum 44x44px)"
```

## Configuration Reference

```yaml
configuration_files:
  
  _config.md:
    frontmatter:
      site_name: "DocsHub"                              # Header text
      tagline: "Your Documentation Hub"                 # Subtitle
      window_title: "DocsHub - Your Documentation Hub"  # Browser tab title
  
  theme.json:
    structure: "Two main sections: light and dark"
    colors: "CSS variable names with hex values"
    customizable_variables:
      - "--bg": "Main background"
      - "--card": "Content card background"
      - "--text": "Primary text color"
      - "--accent": "Link and highlight color"
      - "--border": "Border/divider color"
      - "--shadow": "Elevation shadow"
  
  folder_index_files:
    frontmatter_options:
      menu_position: "Integer (lower appears first)"
      menu_title: "Custom display name in menu"
      menu_hidden: "true/false to hide from navigation"
```

## Error Handling

```yaml
error_handling:
  
  file_not_found:
    trigger: "Requested markdown file doesn't exist"
    display: "404 - Page Not Found error message"
    action: "Shows link back to home"
  
  fetch_failures:
    trigger: "Network error or file fetch fails"
    display: "Error message in content area"
    action: "Logged to console for debugging"
  
  malformed_markdown:
    trigger: "Invalid markdown syntax"
    handling: "marked.js processes gracefully"
    display: "Best-effort rendering"
  
  missing_config:
    trigger: "_config.md, _header.md, or _footer.md not found"
    handling: "Uses default values or skips loading"
    fallback: "Site still functions with defaults"
```

## Maintenance and Extensibility

```yaml
common_tasks:
  
  add_new_page:
    steps:
      - "Create .md file in appropriate content folder"
      - "Update content/.manifest.json with new file path (optional but recommended)"
      - "Content automatically discovered on next load"
      - "No restart or rebuild needed"
  
  customize_colors:
    method: "Edit content/theme.json"
    format: "Light and dark color schemes"
    immediate_effect: "Applies on next page load"
  
  change_site_metadata:
    method: "Edit content/_config.md frontmatter"
    options:
      - "site_name"
      - "tagline"
      - "window_title"
  
  add_footer_content:
    method: "Edit content/_footer.md"
    format: "Markdown (converted to HTML)"
    updates_on: "Automatic on next load"
  
  add_custom_logo:
    method: "Place logo.svg in content/ folder"
    format: "SVG file (32x32 pixels)"
    location: "Displayed in header next to title"
  
  update_favicon:
    method: "Replace content/favicon.svg"
    format: "SVG or other image format (32x32 recommended)"
    location: "Loaded from content/ directory"
    reference: "Linked in HTML <head> with correct path"

future_enhancements:
  - "Full-text search pre-processing and indexing"
  - "Table of contents generation from headers"
  - "Multi-language support"
  - "Analytics integration"
  - "Comments/discussion system"
  - "Version history/git integration"
  - "Advanced markdown features (tabs, collapsible sections)"
```

---

**Document Version**: 1.0  
**Last Updated**: November 2025  
**System**: DocsHub SPA

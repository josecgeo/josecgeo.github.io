---
type: "site_theme"
description: "Color scheme and styling configuration"
---

# Theme Configuration

This file defines the visual appearance of DocsHub in both light and dark modes.

## Light Mode Colors

```yaml
light_mode:
  background: "#fafbfc"                   # Main page background
  card_background: "#ffffff"              # Content card background
  text_color: "#111827"                   # Primary text
  secondary_text: "#374151"               # Secondary text (muted)
  accent_color: "#3b82f6"                 # Links and highlights
  accent_hover: "#2563eb"                 # Accent on hover
  navigation_bg: "#ffffff"                # Navigation bar background
  border_color: "#e5e7eb"                 # Border lines
  border_light: "#f3f4f6"                 # Light borders
  shadow: "0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06)"
  shadow_medium: "0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)"
  shadow_large: "0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05)"
  corner_radius: "12px"                   # Rounded corners
  small_radius: "8px"                     # Small rounded corners
  transition_speed: "all 0.2s"            # Animation speed
```

## Dark Mode Colors

```yaml
dark_mode:
  background: "#0f172a"                   # Dark background
  card_background: "#1e293b"              # Dark card background
  text_color: "#f1f5f9"                   # Light text
  secondary_text: "#cbd5e1"               # Light secondary text
  accent_color: "#60a5fa"                 # Light accent
  accent_hover: "#3b82f6"                 # Light accent hover
  navigation_bg: "#1e293b"                # Dark navigation
  border_color: "#334155"                 # Dark border
  border_light: "#1e293b"                 # Dark light border
  shadow: "0 1px 3px 0 rgba(0, 0, 0, 0.3), 0 1px 2px 0 rgba(0, 0, 0, 0.2)"
  shadow_medium: "0 4px 6px -1px rgba(0, 0, 0, 0.3), 0 2px 4px -1px rgba(0, 0, 0, 0.2)"
  shadow_large: "0 10px 15px -3px rgba(0, 0, 0, 0.3), 0 4px 6px -2px rgba(0, 0, 0, 0.2)"
  corner_radius: "12px"
  small_radius: "8px"
  transition_speed: "all 0.2s"
```

## How to Customize

1. Edit the color hex values above
2. Save the file
3. Refresh your browser to see changes immediately
4. No code changes required!

## Color Tips

- **Accent Color**: Used for links, buttons, and highlights
- **Text Color**: Main text throughout the site
- **Background**: Page background color
- **Border Color**: Dividing lines between sections
- **Shadow**: Depth and elevation effects

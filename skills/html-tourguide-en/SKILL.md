---
name: html-tourguide-en
description: Generate a minimal, mobile-first, offline HTML travel guide from a route, with collapsible destination cards and direct map navigation.
---

# HTML Tour Guide EN

Turn a travel route into a minimal, mobile-first offline HTML guide.

## When to use

- The user wants to turn an itinerary, city walk, themed route, or day trip into an HTML page
- The page should work well on mobile, be easy to share, and ideally work offline
- Each stop should have collapsible details and a visible navigation button

## Working principles

- Default to minimal output and show only what matters right now
- Keep the visual style calm and restrained, like Apple Notes / Apple Maps cards
- Write in an observational tone, not as a long-form travel article
- Avoid asking follow-up questions unless missing information blocks generation
- The result must be a single HTML file with CSS and JavaScript embedded in the same file

## Recommended input

Prefer a structure like this:

```yaml
title: ""
city: ""
duration: ""
transportation: ""
route_theme: ""
navigation_profile: "auto"
stops:
  - name: ""
    map_keyword: ""
    summary: ""
    context: ""
    observe:
      - ""
      - ""
    lat: 0
    lon: 0
    coord_type: "gcj02"
    nav_mode: "walk"
```

If fields are missing, infer reasonable defaults from context.

## Page structure

By default, the page should contain only two main sections:

1. Overview
2. Route List

Do not add these sections by default:

- Further reading
- Photography tips
- Food recommendations
- Packing checklist
- References

Only add them if the user explicitly asks.

## Overview

Keep the overview short and easy to scan:

- Guide title
- One-sentence theme
- City
- Duration
- Transport mode
- Route order

## Route list

Each destination should be rendered as a collapsible card row.

### Collapsed state

Show only:

- Destination name
- Navigation button

### Expanded state

Show only:

- One-sentence summary
- Short background
- Observation keywords

Do not write long article-style descriptions.

### Interaction rules

- Tapping a destination row expands or collapses details
- Tapping the navigation button only launches navigation
- Only one destination should be open at a time by default
- Keep motion lightweight and avoid complex animations
- Do not show a multi-map picker by default

## Navigation strategy

Default `navigation_profile` to `auto`.

- If coordinates are available, prefer route planning
- If coordinates are missing, prefer keyword search
- Use GCJ-02 for mainland China when possible
- If coordinates are uncertain, prefer search over guessing

See [navigation reference](references/navigation.md) for URL patterns and fallback behavior.

## Writing style

Keep the tone concise, restrained, and observational.

Preferred words:

- route
- observe
- neighborhood
- node
- trace
- change
- migration
- renewal
- site
- transition

Avoid overusing:

- you must
- you should definitely
- extremely important
- think deeply
- highly representative
- must-see

## Visual style

Use a light card-based layout with system fonts and no external dependencies.

Suggested variables:

```css
:root {
  --bg: #f5f5f7;
  --card: #ffffff;
  --text: #1d1d1f;
  --muted: #6e6e73;
  --line: rgba(0, 0, 0, 0.08);
  --accent: #007aff;
  --radius: 22px;
}
```

Dark mode is fine, but it should not compromise the default clean look.

## Preflight checklist

- The page has only Overview and Route List
- Every destination is collapsed by default
- Collapsed rows show only the stop name and navigation button
- Navigation button does not expand or collapse the row
- The page is a single HTML file
- The page can be opened offline
- No external CSS or JavaScript libraries are required
- Every destination has a map keyword
- Add coordinates when you can
- Keep the text short and avoid long-form travel prose

## Output

When finished, provide:

1. The generated HTML file
2. A short note explaining how to open and use it


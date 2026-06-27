# TOURGUIDE-WITH-HTML

## Purpose

Turn a travel route into a minimal, mobile-first offline HTML guide.

This skill is not intended to generate a long travel article. Its purpose is to reduce app switching, visual noise, and operational friction during a trip. It turns a route into a lightweight mobile guide: users can open the page, view the overview, browse the route, expand destination details, and tap one navigation button to launch map navigation as directly as possible.

The final HTML should feel like a quiet, restrained, and clear mobile guide card, not a complex travel website.

---

## Core Positioning

This skill is designed for:

* organizing an existing travel route
* creating a lightweight city walk guide
* turning a themed route into a mobile HTML page
* sharing a simple offline guide with friends or family
* reducing switching between notes, screenshots, map apps, and documents
* creating a self-guided tour that can be opened offline

This skill can help refine a route, but its core output is an HTML guide.

---

## Design Philosophy

### 1. Minimal by default

The default interface should only show what the traveler needs immediately:

* What is this route?
* What is the next stop?
* How do I start navigation?

Additional content should be collapsed by default and shown only when the user expands a destination.

---

### 2. Apple-like visual style

The final HTML page should feel clean, calm, and premium.

The visual style should be inspired by Apple Notes, Apple Maps, and iOS card interfaces:

* soft light gray background
* white rounded cards
* generous spacing
* system fonts
* subtle borders
* very soft shadows
* clear typography hierarchy
* restrained color usage
* simple button design

Avoid:

* complex gradients
* decorative hero images
* complicated navigation bars
* excessive emoji
* dense information blocks
* loud travel-app style interfaces
* long essay-style destination descriptions

---

### 3. Leave space for observation

Do not over-explain every destination.

A good guide provides enough context, but does not complete all the thinking for the traveler. It should provide concise context and observation keywords so the traveler can observe, connect, and reflect on site.

---

## When to Use This Skill

Use this skill when the user wants to:

* turn a travel plan into an HTML guide
* organize a one-day route
* create a city walk guide
* add map navigation buttons to destinations
* generate a mobile-friendly offline page
* share a simple route with others
* create a themed self-guided travel route

Typical scenarios include:

* book-inspired routes
* historical city routes
* museum routes
* neighborhood walks
* food walks
* architecture walks
* film location routes
* cultural or social observation city walks

---

## Input Information

The user may provide:

```yaml
title:
city:
duration:
transportation:
route_theme:
navigation_profile:
stops:
  - name:
    map_keyword:
    summary:
    context:
    observe:
    lat:
    lon:
    coord_type:
    nav_mode:
```

If some information is missing, infer reasonable defaults from the context.

Do not ask frequent clarification questions unless missing information prevents generating a usable guide.

---

## Recommended Data Structure

Before generating the HTML, organize the route into the following structure:

```yaml
guide:
  title: "Route Title"
  theme: "One-sentence theme"
  city: "City Name"
  duration: "1 day"
  transportation: "Metro + walking"
  route_summary: "Stop A → Stop B → Stop C"
  navigation_profile: "auto"

stops:
  - name: "Destination Name"
    map_keyword: "City + Destination Name"
    summary: "One concise sentence explaining why this stop matters."
    context: "Short background paragraph, preferably within 80-150 words."
    observe:
      - "Observation keyword 1"
      - "Observation keyword 2"
      - "Observation keyword 3"
      - "Observation keyword 4"
    lat: 39.849321
    lon: 116.398456
    coord_type: "gcj02"
    nav_mode: "walk"
```

Keep the data structure simple.

Do not add the following fields by default:

* long_description
* photo_tips
* packing_list
* detailed_history
* complex_score
* excessive_recommendations

Only add these when the user explicitly requests them.

---

## Content Rules

### Overview Section

The overview section should include only the most essential information:

* guide title
* one-sentence theme
* city
* duration
* transportation mode
* route order

Example:

```text
Zhejiang Village: A One-Day South Beijing Walk

A route about migration, clothing markets, and urban renewal.

City: Beijing
Duration: 1 day
Transport: Metro + walking
Route: Dahongmen → Haihutun → Dongluoyuan → Shiliuzhuang → Dashilar → Tianqiao
```

Keep the overview concise. Do not turn it into a long travel article introduction.

---

### Destination Content

Each destination should include:

1. Destination name
2. Navigation button
3. One-sentence summary
4. Short background context
5. Observation keywords

Collapsed state:

```text
Dahongmen                                      Navigate
```

Expanded state:

```text
Dahongmen                                      Navigate

A core node of the clothing wholesale network.

This area was once an important part of Beijing’s southern clothing wholesale and production network. Walking through the neighborhood, observe the relationship between markets, logistics, residential space, and urban renewal.

Observe:
wholesale market / logistics / South Beijing / industrial migration
```

---

### Writing Style

Use concise, restrained, calm, and observational language.

Preferred:

```text
A core node of the clothing wholesale network.
```

Avoid:

```text
This is an extremely important place that fully demonstrates the complex social transformation of China’s urbanization process since the Reform and Opening period...
```

Recommended words:

* route
* observe
* neighborhood
* node
* trace
* change
* migration
* renewal
* site
* transition

Avoid overusing:

* you must
* you definitely should
* extremely important
* think deeply
* fully demonstrates
* highly representative
* must-see

---

## HTML Output Requirements

Generate a single-file HTML page.

The HTML should:

* be openable offline after saving
* be mobile-first
* use no external CSS libraries
* use no external JavaScript libraries
* use system fonts
* support responsive layout
* include one navigation button for each destination
* keep all CSS and JavaScript inside the same HTML file

The page should not rely on external network resources except when the user taps a navigation button or opens a web map fallback.

---

## Page Structure

The final page should contain only two main sections by default:

```text
1. Overview
2. Route List
```

Do not add too many default sections.

For example, do not add these sections unless the user explicitly asks:

* further reading
* photography tips
* food recommendations
* packing checklist
* references

---

## Section 1: Overview

The overview section should be visually prominent but compact.

Recommended structure:

```text
[Guide Title]

[One-sentence theme]

City        Beijing
Duration    1 day
Transport   Metro + walking

Route
Stop A → Stop B → Stop C → Stop D
```

Use a card layout.

---

## Section 2: Route List

The route list is the core of the page.

Each destination should appear as a collapsible row card.

### Collapsed State

Each row should show only:

* left side: destination name
* right side: navigation button

Example:

```text
Dahongmen                                      Navigate
Haihutun                                      Navigate
Dongluoyuan                                   Navigate
Shiliuzhuang                                  Navigate
Dashilar                                      Navigate
Tianqiao                                      Navigate
```

### Expanded State

When a row is tapped, show:

* one-sentence summary
* short background context
* observation keywords

Expanded content must be short and should not become a long article.

---

## Interaction Rules

* Tapping a destination row expands or collapses its details.
* Tapping the “Navigate” button attempts to open map navigation.
* Tapping the “Navigate” button must not expand or collapse the row.
* By default, only one destination should be expanded at a time.
* Interactions should feel lightweight, quick, and simple.
* Do not show a multi-map picker by default.

JavaScript should only be used for the collapsible list and navigation launch behavior.

---

## Navigation Strategy

Navigation should remain simple.

Each destination should show only one visible “Navigate” button.

Do not show a multi-map selection panel by default.

### Default Navigation Behavior

Use the following setting:

```yaml
navigation_profile: auto
```

Available values:

```yaml
auto:
  Android: try to open Amap directly, then fallback to Google Maps.
  iOS: try to open Amap first, then fallback to Apple Maps.
  Other: open a web map fallback.

android_amap_google:
  Android-specific strategy. Try Amap first, then fallback to Google Maps.

ios_amap_system:
  iOS-specific strategy. Try Amap first, then fallback to Apple Maps.
```

### Important Limitation

A normal HTML page cannot reliably detect which map apps are installed on the user’s phone, and it cannot fully bypass Android or iOS security confirmation dialogs.

The guide should try to launch a map app directly, but the system or browser may still:

* show a confirmation dialog
* open a browser first
* block external app launch
* fallback to a web map
* fail silently in some in-app browsers

This is expected behavior caused by mobile operating system and browser security restrictions.

---

## Navigation Data Requirements

To make direct route navigation more reliable, each destination should preferably include coordinates:

```yaml
stops:
  - name: "Destination Name"
    map_keyword: "City + Destination Name"
    lat: 39.849321
    lon: 116.398456
    coord_type: "gcj02"
    nav_mode: "walk"
```

If `lat` and `lon` are provided:

* Android should attempt Amap route planning first, then fallback to Google Maps.
* iOS should attempt Amap route planning first, then fallback to Apple Maps.

If coordinates are missing:

* Android should fallback to Amap place search, with Google Maps as the failure fallback.
* iOS should fallback to Amap place search, with Apple Maps as the failure fallback.

For mainland China routes, prefer GCJ-02 coordinates for Amap.

If coordinates are uncertain, use keyword search first to avoid inaccurate navigation locations.

---

## Map Launch Rules

### Android

On Android, tapping the navigation button should use an Android Intent URL to directly attempt Amap route planning.

Amap package name:

```text
com.autonavi.minimap
```

Use walking mode by default for city walks:

```text
t=2
```

If Amap is not installed or cannot be launched, the Android Intent `browser_fallback_url` should fallback to Google Maps.

Android fallback should use Google Maps directions:

```text
https://www.google.com/maps/dir/?api=1&destination={encoded_destination}&travelmode=walking
```

If coordinates are missing, use the destination keyword:

```text
https://www.google.com/maps/dir/?api=1&destination={encoded_keyword}&travelmode=walking
```

---

### iOS

On iOS, tapping the navigation button should:

1. Try to open Amap using the `iosamap://` URL scheme.
2. If Amap does not open, fallback to Apple Maps after a short delay.

Do not show a map picker by default.

---

### Other Devices

Use a web map fallback.

For mainland China routes, Amap web fallback may be used:

```text
https://uri.amap.com/search?keyword={encoded_keyword}&callnative=1
```

For international routes, Google Maps or Apple Maps web links may be used as appropriate.

---

## Default Visual Specification

Suggested CSS variables:

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

Typography:

```css
font-family: -apple-system, BlinkMacSystemFont, "SF Pro Text", "Helvetica Neue", Arial, sans-serif;
```

Layout recommendations:

* max width: 760px
* mobile padding: 18px
* card radius: 20-24px
* button radius: 999px
* avoid strong shadows
* prefer subtle borders
* line height: 1.55-1.7
* clear headings, restrained body text
* generous spacing

---

## Dark Mode

Support system dark mode with `prefers-color-scheme`.

Example:

```css
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #000000;
    --card: #1c1c1e;
    --text: #f5f5f7;
    --muted: #a1a1a6;
    --line: rgba(255, 255, 255, 0.12);
    --accent: #0a84ff;
  }
}
```

---

## HTML Structure Reference

Use a structure similar to this:

```html
<div class="stop" data-stop>
  <div class="stop-header">
    <button class="stop-toggle">
      <span class="stop-name">Dahongmen</span>
    </button>
    <button
      class="nav-button"
      onclick='openNavigation({
        name: "Dahongmen",
        map_keyword: "Beijing Dahongmen",
        lat: 39.849321,
        lon: 116.398456,
        coord_type: "gcj02",
        nav_mode: "walk"
      }, event)'
    >
      Navigate
    </button>
  </div>

  <div class="stop-detail">
    <p class="summary">A core node of the clothing wholesale network.</p>
    <p class="context">This area was once an important part of Beijing’s southern clothing wholesale and production network.</p>
    <div class="keywords">
      <span>wholesale market</span>
      <span>logistics</span>
      <span>South Beijing</span>
      <span>industrial migration</span>
    </div>
  </div>
</div>
```

Collapsible interaction reference:

```javascript
document.querySelectorAll("[data-stop]").forEach((stop) => {
  const toggle = stop.querySelector(".stop-toggle");

  toggle.addEventListener("click", () => {
    document.querySelectorAll("[data-stop]").forEach((item) => {
      if (item !== stop) item.classList.remove("open");
    });
    stop.classList.toggle("open");
  });
});
```

Navigation launch reference:

```javascript
const NAV_PROFILE = "auto";

function enc(value) {
  return encodeURIComponent(value || "");
}

function hasCoord(stop) {
  return stop.lat && stop.lon;
}

function getModeCode(stop) {
  const mode = stop.nav_mode || "walk";
  if (mode === "drive") return "0";
  if (mode === "bus") return "1";
  if (mode === "walk") return "2";
  if (mode === "ride") return "3";
  return "2";
}

function getGoogleTravelMode(stop) {
  const mode = stop.nav_mode || "walk";
  if (mode === "drive") return "driving";
  if (mode === "bus") return "transit";
  if (mode === "walk") return "walking";
  if (mode === "ride") return "bicycling";
  return "walking";
}

function createGoogleMapsFallback(stop) {
  const destination = hasCoord(stop)
    ? stop.lat + "," + stop.lon
    : (stop.map_keyword || stop.name);

  return (
    "https://www.google.com/maps/dir/?" +
    "api=1" +
    "&destination=" + enc(destination) +
    "&travelmode=" + getGoogleTravelMode(stop)
  );
}

function createAmapWebFallback(stop) {
  const keyword = stop.map_keyword || stop.name;

  if (hasCoord(stop)) {
    return (
      "https://uri.amap.com/navigation" +
      "?from=" +
      "&to=" + stop.lon + "," + stop.lat + "," + enc(stop.name) +
      "&mode=walk" +
      "&src=tourguide" +
      "&coordinate=gaode" +
      "&callnative=1"
    );
  }

  return "https://uri.amap.com/search?keyword=" + enc(keyword) + "&callnative=1";
}

function createAndroidAmapRoute(stop) {
  const fallback = encodeURIComponent(createGoogleMapsFallback(stop));

  if (!hasCoord(stop)) {
    return (
      "intent://poi" +
      "?sourceApplication=tourguide" +
      "&keywords=" + enc(stop.map_keyword || stop.name) +
      "&dev=0" +
      "#Intent;" +
      "scheme=androidamap;" +
      "package=com.autonavi.minimap;" +
      "S.browser_fallback_url=" + fallback + ";" +
      "end"
    );
  }

  return (
    "intent://route/plan/" +
    "?sourceApplication=tourguide" +
    "&sid=" +
    "&slat=" +
    "&slon=" +
    "&sname=" + enc("My Location") +
    "&did=" +
    "&dlat=" + stop.lat +
    "&dlon=" + stop.lon +
    "&dname=" + enc(stop.name) +
    "&dev=0" +
    "&t=" + getModeCode(stop) +
    "#Intent;" +
    "scheme=amapuri;" +
    "package=com.autonavi.minimap;" +
    "S.browser_fallback_url=" + fallback + ";" +
    "end"
  );
}

function createIOSAmapRoute(stop) {
  if (!hasCoord(stop)) {
    return (
      "iosamap://poi" +
      "?sourceApplication=tourguide" +
      "&keywords=" + enc(stop.map_keyword || stop.name) +
      "&dev=0"
    );
  }

  return (
    "iosamap://path" +
    "?sourceApplication=tourguide" +
    "&sid=" +
    "&slat=" +
    "&slon=" +
    "&sname=" + enc("My Location") +
    "&did=" +
    "&dlat=" + stop.lat +
    "&dlon=" + stop.lon +
    "&dname=" + enc(stop.name) +
    "&dev=0" +
    "&t=" + getModeCode(stop)
  );
}

function createAppleMapsRoute(stop) {
  if (hasCoord(stop)) {
    return (
      "https://maps.apple.com/?" +
      "daddr=" + enc(stop.lat + "," + stop.lon) +
      "&q=" + enc(stop.name) +
      "&dirflg=w"
    );
  }

  return (
    "https://maps.apple.com/?" +
    "daddr=" + enc(stop.map_keyword || stop.name) +
    "&dirflg=w"
  );
}

function openIOSNavigation(stop) {
  const amapUrl = createIOSAmapRoute(stop);
  const appleUrl = createAppleMapsRoute(stop);

  const start = Date.now();

  window.location.href = amapUrl;

  setTimeout(() => {
    const elapsed = Date.now() - start;

    if (elapsed < 1600 && document.visibilityState === "visible") {
      window.location.href = appleUrl;
    }
  }, 900);
}

function openNavigation(stop, event) {
  if (event) {
    event.preventDefault();
    event.stopPropagation();
  }

  const ua = navigator.userAgent || "";
  const isAndroid = /Android/i.test(ua);
  const isIOS = /iPhone|iPad|iPod/i.test(ua);

  if (
    NAV_PROFILE === "android_amap_google" ||
    (NAV_PROFILE === "auto" && isAndroid)
  ) {
    window.location.href = createAndroidAmapRoute(stop);
    return;
  }

  if (
    NAV_PROFILE === "ios_amap_system" ||
    (NAV_PROFILE === "auto" && isIOS)
  ) {
    openIOSNavigation(stop);
    return;
  }

  window.location.href = createAmapWebFallback(stop);
}
```

---

## Quality Checklist

Before finalizing the HTML, check:

* The page has only two main sections: Overview and Route List.
* Each destination is collapsed by default.
* Collapsed rows show only destination name and navigation button.
* Destination details only appear after the row is expanded.
* The navigation button tries to open map navigation directly.
* The navigation button does not trigger row expansion or collapse.
* No multi-map selection panel is shown by default.
* Android attempts to open Amap directly.
* Android falls back to Google Maps if Amap cannot be opened.
* iOS attempts to open Amap first.
* iOS falls back to Apple Maps if Amap cannot be opened.
* Each destination has a map keyword.
* Coordinates are included when available.
* If coordinates are uncertain, keyword search is preferred.
* Destination text is concise.
* No long travel article is shown by default.
* The visual style feels clean, calm, and premium.
* The page is mobile-friendly.
* The HTML is a single file.
* The page can be opened offline.
* The user can understand the route in less than 10 seconds.

---

## Example User Request

```text
Please turn this Beijing route into a minimal offline HTML guide:

Title: Zhejiang Village: A One-Day South Beijing Walk
City: Beijing
Duration: 1 day
Transport: Metro + walking
Navigation profile: auto
Stops:
- Dahongmen
- Haihutun
- Dongluoyuan
- Shiliuzhuang
- Dashilar
- Tianqiao
```

Expected output:

* a complete single-file HTML page
* Apple-like minimal UI
* Overview section
* collapsible route list
* one navigation button per stop
* Android Amap-first and Google Maps fallback behavior
* iOS Amap-first and Apple Maps fallback behavior
* concise destination context
* observation keywords

---

## Final Output Format

When completing the task, provide:

1. The generated HTML file
2. A short usage note

Example:

```text
Done. Open the HTML file on your phone. Tap a destination row to expand details, or tap “Navigate” to try opening map navigation.
```

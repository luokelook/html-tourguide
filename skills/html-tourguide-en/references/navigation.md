# Navigation Reference

Use this file when you need the map navigation behavior for the HTML guide.

## Navigation profile

- `auto`
- `android_amap_google`
- `ios_amap_system`

Default should be `auto`.

## Common rules

- Prefer coordinates when both `lat` and `lon` are available
- Prefer `map_keyword` or `name` when coordinates are missing or uncertain
- Use `gcj02` coordinates for mainland China when possible
- Keep the navigation UI to one button per stop
- Do not add a map picker by default

## Android

Preferred order:

1. Try Amap route planning through an intent URL
2. If that fails, fall back to Google Maps

If coordinates exist, use route planning.

If coordinates do not exist, use keyword search.

Google Maps fallback pattern:

```text
https://www.google.com/maps/dir/?api=1&destination={encoded_destination}&travelmode=walking
```

## iOS

Preferred order:

1. Try `iosamap://`
2. If that fails, fall back to Apple Maps

If coordinates exist, build a route URL.

If coordinates do not exist, use keyword search.

Apple Maps fallback pattern:

```text
https://maps.apple.com/?daddr={encoded_destination}&dirflg=w
```

## Web fallback

For mainland China keyword search:

```text
https://uri.amap.com/search?keyword={encoded_keyword}&callnative=1
```

## Implementation notes

- Use `event.preventDefault()` and `event.stopPropagation()` on the navigation button
- Keep the collapse behavior independent from navigation
- A small delay-based fallback for iOS is acceptable


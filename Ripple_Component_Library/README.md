# Ripple Mobile Component Library · V2

An interactive mobile UI library rebuilt from the selected four-screen visual reference. The library preserves Ripple's product rules while adopting the new warm editorial direction: cream paper surfaces, tomato-red actions, ink-black typography, hand-painted activity art, thin borders, and generous rounded geometry.

## Preview

Open `index.html` directly, or run a small local server from this folder:

```sh
python3 -m http.server 4173
```

Then open `http://localhost:4173`.

## Included

- Four 390 × 844-oriented product screens: welcome, activity feed, activity details, and group chat
- Primary, pressed, loading, disabled, and secondary buttons
- Segmented navigation, filter chips, bottom navigation, and status badges
- Activity rows, pinned activity card, metadata, host identity, and anonymous message components
- Default, focus, filled, and error form patterns
- Portable `tokens.json` with colors, typography, spacing, radii, and control sizes
- Responsive component documentation below the screen gallery

## Core interactions

- Get Started moves into the Discover experience
- Feed cards open the activity-details example
- Favorite controls toggle saved state
- Join Activity updates counts and becomes Open Group
- Suggested replies fill the composer; Send appends an anonymous message
- Segmented controls, filters, and bottom navigation expose active states
- Palette swatches and the header action copy design tokens

## Original generated artwork

- `assets/ripple-wordmark.png`
- `assets/onboarding-community.png`
- `assets/coffee-social.png`
- `assets/sunset-hike.png`
- `assets/indie-music.png`
- `assets/pickleball.png`

The artwork was generated specifically for this library from the reference's mid-century editorial direction. The implementation uses Iconoir for product icons and DiceBear for demo-only anonymous avatars.

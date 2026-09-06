# Ripple — Interactive Mobile App Demo

Ripple is a front-end prototype for discovering real-world activities and joining anonymous, activity-based group chats. It combines Ripple’s warm, illustrated visual language with an iPhone-style mobile interface.

**Live demo:** [qinghao-f.github.io/ripple](https://qinghao-f.github.io/ripple/)

## What you can try

- Complete the onboarding flow: phone number, verification code, contacts permission, anonymous identity, age check, and interests.
- Browse activities in **Poster Board**, **Map**, and **My Plans**.
- Open an activity, review its details, and confirm joining it.
- Create a new activity, generate a poster, preview it, and publish it.
- Use anonymous activity group chats, suggested replies, and read-only cancelled chats.
- Inspect loading, empty, error, disabled, and confirmation states throughout the demo.

This is a prototype only. Phone verification, contacts, location, poster generation, and chats are simulated; no real personal data is collected or sent.

## Run locally

No build step or package installation is required. Serve the project folder with any static web server.

```sh
git clone https://github.com/Qinghao-F/ripple.git
```

In the cloned repository folder, run:

```sh
python3 -m http.server 4177
```

Then open [http://localhost:4177](http://localhost:4177) in a browser.

To enter the demo, use:

- Mobile number: `0412 345 678`
- Verification code: `123456`

## Design system

The app is built from the included [Ripple Component Library](Ripple_Component_Library/README.md). Its tokens, styles, wordmark, illustrations, activity artwork, spacing, radii, shadows, and warm colour palette are the source of truth for this demo.

The iPhone shell and app-specific layouts—such as the map, confirmation sheets, calendar, and onboarding flow—are composed from those existing visual rules rather than introducing a separate design system.

## Project structure

```text
.
├── index.html                    # App entry point and iPhone preview shell
├── app.js                        # Screens, state, and demo interactions
├── styles.css                    # Ripple app layouts and components
├── ios-shell.css                 # iPhone safe-area and iOS interaction refinements
├── welcome.css                   # Welcome screen styling
├── Ripple_Component_Library/
│   ├── README.md                 # Component library guidance
│   ├── tokens.json               # Design tokens
│   ├── styles.css                # Shared component styles
│   └── assets/                   # Brand and activity artwork
└── IOS_HIG_REVIEW.md             # iOS layout and accessibility review notes
```

## Interaction notes

- Horizontal swipe works on **Poster Board / Map / My Plans** and **New / My Posts** tab strips.
- Map filters stay on the map; activity markers update the preview card.
- Confirmation sheets keep the descriptive copy, primary action, and defer action in a clear top-to-bottom order.
- All primary controls are designed with at least a 44 × 44 pt touch target in the 390 × 844 pt iPhone preview.

## Browser support

Use a current version of Chrome, Safari, Edge, or Firefox. The prototype is optimised for a 390 × 844 pt iPhone viewport and also adapts to smaller mobile screens.

## Credits

Ripple brand assets and component patterns are included in this repository for this demo. Iconography is provided through [Iconoir](https://iconoir.com/).

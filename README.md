# Ripple Interactive Demo — Pre-iOS version

This is the preserved visual/interaction version from immediately before the iOS Human Interface Guidelines rework. It keeps the earlier Ripple web-mobile presentation, including Manrope and Iconoir.

The demo now includes an iPhone 15 / 14 / 13 preview shell and layout corrections in `ios-shell.css`; the historical visual language and interaction model remain otherwise unchanged. See `IOS_HIG_REVIEW.md` for the final checklist.

Run locally from the parent `MIT` folder so the demo can load the component-library assets:

```sh
cd /Users/fangqinghao/Desktop/MIT
python3 -m http.server 4174
```

Then open `http://localhost:4174/Ripple_Demo_App_Pre_iOS/`.

## Page structure

- Registration: phone verification, contacts permission, anonymous identity, eligibility, interests
- Discover: Poster Board, Map, My Plans, activity detail
- Create: New Activity, poster preview/publish, My Posts, activity editor
- Chats: activity-only chat list and group conversation

## Component reuse

The demo loads the Ripple library stylesheet and reuses its primary/secondary actions, segmented navigation, filter chips, activity/pinned cards, status badges, form fields, bottom navigation, chat messages and composer. It also uses only the library wordmark and activity/illustration assets.

## Intentional extensions

The library does not include registration, calendar, map, editor, sheets, or poster-board components. These are composed from its tokens and existing card, chip, field, button and status patterns. No additional palette, font family, spacing scale, radius scale, shadow treatment, or illustration is introduced.

## Interactive states

- Buttons: hover, pressed, loading, disabled
- Inputs: empty, focused, filled, inline error
- Discover: initial loading, load more, empty filter result, network error, end of results, joined, full, cancelled
- Create: validation, disabled publishing, simulated poster generation, draft/published editor states
- Chats: suggested reply, message send, cancelled read-only state

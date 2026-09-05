# Ripple iOS layout review

## Final result

The Pre-iOS demo now renders inside a 390 × 844 pt iPhone-style frame while retaining the Ripple palette, wordmark, illustrations, and activity experience.

| Review item | Result |
| --- | --- |
| Phone canvas | Pass — 390 × 844 pt outer frame |
| Status bar | Pass — 47 pt, contained inside the phone |
| App content region | Pass — 763 pt between status bar and Home Indicator |
| Home Indicator area | Pass — 34 pt, contained inside the phone |
| Tab Bar clearance | Pass — 50 pt reserved so scroll content ends above the Tab Bar |
| Page gutters | Pass — 16 pt; Poster Board content width is 358 pt |
| Poster Board columns | Pass — two equal 173 pt columns, 12 pt column gap |
| Poster Board rows | Pass — 12 pt gap within each column; first row top edges aligned, later rows flow independently |
| Card typography | Pass — consistent title, metadata, and footer sizing; natural card heights |
| Icon sizing | Pass — navigation 20 pt, metadata 16 pt, Tab Bar 24 pt, empty-state illustration icon 48 pt |
| Touch targets | Pass — visible controls are at least 44 × 44 pt after the final CSS guard |
| Registration controls | Pass — phone field, country code, OTP cells, and Continue / Verify stay inside the 358 pt content column |
| Country code | Pass — +61 / +1 / +44 now use an app-owned Sheet with 17 pt labels and 48 pt options |
| Date of birth | Pass — app-owned popover directly below the field, 358 pt inner width, 17 pt controls, and 44 pt hit areas |
| Chats filter | Pass — All / Unread / Hosting remain within the phone and can scroll horizontally if needed |
| Chat composer | Pass — composer ends at 818 pt, above the 834 pt app boundary and 34 pt Home Indicator area |
| Chat messages | Pass — incoming message bubbles use a borderless transparent surface; Ripple red is retained for own messages |
| Swipe navigation | Pass — horizontal swipe on the Discover / Create surfaces switches their tab views |
| Onboarding hierarchy | Pass — larger Ripple mark, lower copy/forms, raised primary action, and centered 17 pt page titles |
| Brand system | Pass — Ripple colors, typography context, wordmark, and supplied artwork retained |
| Loading / empty / error states | Pass — existing states preserved and remain reachable in the demo |
| Accessibility labels | Pass in code review — status bar, demo guide, form controls, and key actions are labelled |

## Remaining manual confirmation

- Test the largest Dynamic Type setting on a physical iPhone.
- Run VoiceOver and verify focus order across the phone frame, navigation, cards, and forms.
- Confirm the status icons and Dynamic Island proportions against the final native device target.
- Confirm the external Manrope/Iconoir assets are available when testing the preserved Pre-iOS version offline.

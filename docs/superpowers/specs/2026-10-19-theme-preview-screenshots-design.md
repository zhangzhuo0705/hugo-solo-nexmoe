# Theme Preview Screenshots Design

## Goal

Replace the stale theme preview images with current, browser-chrome-free captures
of the deployed example site that satisfy the Hugo Themes media requirements.

## Source and Page State

Capture the deployed home page at:

`https://zhangzhuo0705.github.io/hugo-solo-nexmoe/`

Each capture starts at the top of the page. The capture process waits for the
document load event, web fonts, avatar, article covers, stylesheets, and initial
Canvas rendering. The result must show the current article titles, real local
landscape covers, and requested avatar. Browser controls, window frames, device
mockups, watermarks, and added labels are excluded.

## Output Files

Create two independent native-viewport PNG captures:

- `images/screenshot.png`: 1500 × 1000 pixels
- `images/tn.png`: 900 × 600 pixels

Both files use the required 3:2 aspect ratio. The thumbnail is captured at its
own 900 × 600 viewport instead of being downscaled from the desktop screenshot,
so it represents the theme's actual layout at that width and keeps text as
readable as possible.

## Capture Method

Use an installed headless Chromium-compatible browser through Playwright or an
equivalent screenshot tool. Set the exact viewport before navigation, disable
browser chrome by using page-level screenshots, wait for network activity to
settle, then verify all visible images report `complete` with a non-zero natural
width. Add a short stabilization delay for the Canvas background and lazy-loaded
cover images before writing the PNG.

If the online page cannot be captured reliably, build and serve the same commit
locally with the production base URL shape, then use the local server. Do not
construct or edit a simulated screenshot.

## Validation

The update is complete when:

- both files decode as PNG;
- `screenshot.png` is exactly 1500 × 1000;
- `tn.png` is exactly 900 × 600;
- both aspect ratios are exactly 3:2;
- visual inspection confirms the current avatar, new article titles, real
  landscape covers, sidebar, and article cards render correctly;
- neither image contains the former placeholder color blocks or old article
  titles;
- `README.md` continues to reference the absolute raw URL for
  `images/screenshot.png`;
- the focused image commit is pushed and both raw GitHub image URLs return the
  new files.

## Delivery

Commit the two PNG replacements together as one focused change. Push only after
dimension, format, visual-content, and repository-diff checks pass.

# Fuel Log 🍳

A single-file, mobile-first food logging habit tracker. No backend, no
build step — everything lives in `index.html`, and your data lives in
your phone's browser `localStorage`.

## Setup (2 minutes)

1. Open `index.html` in a text editor.
2. Near the top of the `<script>` block, find:
   ```js
   const GOOGLE_PHOTOS_ALBUM_URL = "https://photos.app.goo.gl/REPLACE_ME_WITH_YOUR_ALBUM_LINK";
   ```
   Paste in your shared Google Photos album link. (You can also just paste
   it into the app itself later, under **⚙️ Settings → Google Photos
   album** — that's saved to localStorage and overrides this constant, so
   you don't have to touch the file again if it changes.)
3. Add a few more rewards to the pool if you like, in **⚙️ Settings →
   Manage rewards** (or edit the `DEFAULT_REWARDS` array in the code).

## Getting it onto your phone

This is hosted at **https://forondaryan.github.io/fuel-log/** (GitHub
Pages, pushed from this folder). For one-tap access, use a **Safari
Bookmark or Favorite** — not "Add to Home Screen."

**Why not Add to Home Screen:** on iOS, an icon added that way can get
launched by Safari in a fully isolated "standalone" storage context,
completely separate from any regular Safari tab — confirmed on-device,
even with every PWA-install signal (manifest.json, capability meta
tags) stripped out of the page. iOS still decided to treat it as an
installed app and gave it empty, disconnected storage. That's an Apple
platform behavior, not something fixable from the page, so it's not
worth the risk for something you need to trust daily.

**Instead:** open the site in Safari → tap the **Share** icon → **Add
Bookmark** (saved in Bookmarks) or **Add to Favorites** (shows as a
tile on Safari's new-tab/start screen — the closest thing to a home
screen icon while guaranteeing it always opens as a normal Safari tab,
sharing storage with every other Safari tab on the device).

It still works completely offline once loaded (nothing calls out to a
server beyond the one-time page fetch and an update check).

## Your data

Everything — logs, streaks, rewards, monthly notes — is stored in
`localStorage` in whatever browser/device you open the file in. That
means:

- **It does not sync between devices** (e.g. phone vs. laptop) unless
  you use Export/Import.
- **Clearing Safari/Chrome site data, or "Clear all data" in Settings,
  deletes it.** Export regularly (Settings → Export JSON) to keep a
  backup — it's a plain JSON file you can keep in iCloud/Dropbox/email
  to yourself.
- **Import** (Settings → Import JSON) fully replaces on-device data with
  the file you pick, so use it for restoring a backup or moving to a
  new phone, not merging.

## How scoring & streaks work

- Breakfast / Lunch / Dinner = 20 pts each, each Snack = 5 pts (max 75/day).
- A day is **complete** once all 3 meals are logged — snacks are bonus,
  never required.
- **Daily streak**: consecutive complete days. One "grace day" per
  calendar month automatically protects the streak from a single missed
  day (it's applied automatically to the first miss each month — no
  action needed from you).
- **Weekly streak**: consecutive weeks with 3+ complete days. Mon/Tue/Wed
  are marked as your "core" days visually, but any 3 days in the week
  count toward the streak.
- Weekly rewards unlock at 3 / 5 / 7 complete days in a week, with a
  celebration animation and a reward picker. Claimed rewards rotate back
  into the pool once every reward at that tier has been used once.

## Editing quotes / moods / slots

Everything customizable lives as constants near the top of the
`<script>` block: `QUOTES`, `MOODS`, `SLOTS`, `DEFAULT_REWARDS`,
`TIER_META`. Nothing else in the file needs to change if you tweak
those.

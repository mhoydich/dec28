# Codex brief: put Serenity on PointCast

Filed 2026-09-25 by Claude Code for Mike. Owner: Codex. Target repo: `mhoydich/pointcast`.

## Goal

Add Serenity, a breathing and meditation app, to PointCast as a static room at `https://pointcast.xyz/serenity/` and list it on the app shelf. Then generate its four time-of-day sky paintings with OpenAI's image model (`plate_generate`) so the room ships with real skies instead of only the canvas-painted fallback.

## Source

- Repo: `https://github.com/mhoydich/dec28`
- Branch: `claude/art-deco-meditation-app-tmkyj`
- Files: `index.html` (one self-contained page) and `fonts/` (3 woff2 files, SIL Open Font License)
- No build step, no network requests, no dependencies.

## Steps

1. In `mhoydich/pointcast`, branch from `main`: `codex/serenity-room`. Do not push to `main`.
2. Copy `index.html` to `public/serenity/index.html` and `fonts/*.woff2` to `public/serenity/fonts/`. Keep the relative `fonts/...` URLs as they are.
3. Add this entry as the first item in `POINTCAST_APPS` in `src/lib/pointcast-apps.ts`:

   ```ts
   {
     slug: 'serenity',
     name: 'Serenity · El Segundo Dunes',
     kicker: 'BREATHE WITH THE MOON · SIX PATTERNS · CHANGES WITH THE HOUR',
     description: 'A breathing room where a painted El Segundo dunescape breathes with you: six patterns, synthesized wind chimes and surf, a field guide of ten local species, and skies painted for each time of day.',
     url: 'https://pointcast.xyz/serenity/',
     path: '/serenity',
     repo: 'https://github.com/mhoydich/pointcast',
     channel: 'CH.ESC',
     kind: 'pointcast',
   },
   ```

4. Generate four sky plates with `plate_generate` and save them as WebP files at `public/serenity/skies/dawn.webp`, `day.webp`, `dusk.webp` and `night.webp`. Use landscape 16:9, around 1600×900, and keep each file under about 400 KB. The page loads `skies/<period>.webp` automatically and falls back to its painted canvas if a file is missing. Each prompt is the shared description followed by one period line:

   **Shared description:** Wide 16:9 landscape painting in a grainy risograph print style with visible stipple and dither texture. Coastal California dunes near El Segundo: a large pale moon centered in the upper middle of the frame, layered hills below it, a few windswept Torrey pines at the far left and right edges, coastal sage and wildflowers in the foreground on reddish earth. Leave the area around the moon calm and uncluttered. No text, no people, no buildings.

   - **dawn:** Dawn palette: indigo fading to rose and apricot near the horizon, soft pink hills, dew on the grass, a few blue butterflies.
   - **day:** Daytime palette: clear coastal blue sky with a faint daytime moon, lavender-gray hills, bright sage green, golden grasses, a few blue butterflies.
   - **dusk:** Golden hour palette: deep violet sky burning to ember orange at the horizon, coral-pink hills, long warm light, the first fireflies.
   - **night:** Night palette: deep ultramarine and violet sky with stars, a glowing sand-colored moon, pink and purple hills, fireflies in the sage.

   The breathing text sits on the moon at about 40% of the height, horizontally centered. Reject any plate where the moon is off-center or text-like marks appear, and regenerate it.

5. Run `npm run build:bare` and confirm `dist/serenity/index.html`, `dist/serenity/fonts/` and `dist/serenity/skies/` exist. Run `npm run audit:agents` if the shelf entry feeds `/agents.json`.
6. Open a draft pull request titled "Add Serenity breathing room to the app shelf".

## Acceptance criteria

- `/serenity/` renders with no console errors, and Serenity appears in the PointCast apps list.
- On a phone-width viewport (390 px) nothing scrolls sideways.
- Each of the four skies shows at its time of day (5–9, 9–17, 17–21, 21–5). A quick check is to override `Date.prototype.getHours` in the browser console and reload.
- Nothing is merged or published without Mike's approval.

## Notes

- The page keeps its state in `localStorage` under keys prefixed `serenity:`, so it won't collide with other rooms on the same origin.
- Claude Code tried to make this change directly but did not get permission to write to `mhoydich/pointcast` from its session. Nothing has been changed in that repo.

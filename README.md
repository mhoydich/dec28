# Serenity · El Segundo Dunes

A breathing and meditation app where the whole landscape breathes with you. A big stippled moon swells as you breathe in and settles as you breathe out, and the dune grass leans with it. The scene is painted live on a canvas in the grainy risograph style of the original reference print.

Open `index.html` in any modern browser. There's no build step and no network access. Fonts ship in `fonts/` (Cormorant Garamond and Karla, both under the SIL Open Font License).

## Time of day

The painting, the bell scale, the wildlife, the suggested pattern and the daily thought all change four times a day.

| Period | Hours | Scene | Suggested pattern |
|---|---|---|---|
| First light | 5–9 | Rose and apricot sky, blue butterflies | Energize |
| Midday | 9–17 | Coastal blue sky, faint daytime moon | Focus |
| Golden hour | 17–21 | Violet to ember sky, first fireflies | Calm |
| Night | 21–5 | Ultramarine sky, stars, fireflies | Sleep |

## Breathing patterns

Calm 4·7·8 · Box 4·4·4·4 · Energize 2·1·4 · Focus 5·2·5·2 · Sleep 4·8·8 · Coastline 5.5·5.5. Tap the moon or press Space to start.

## Features

- **Abundance.** A money counter that only goes up: a slow drip that speeds up while you practice, $0.17 per breath cycle, and milestone messages.
- **Field guide to the dunes.** Every three breaths you spot a real local species, starting with the endangered El Segundo blue butterfly and the seacliff buckwheat it depends on.
- **Wind chimes in the pines.** Seven synthesized brass bells on a pine bough. Strike them, drag to strum, or let the breeze play them. The breeze blows harder while you breathe out.
- **Soundscape.** Synthesized surf, plus songbirds by day and crickets after dark. No audio files are used.
- **Give it to the wind.** Type what's weighing on you and the letters blow away like seeds. Nothing is saved.
- **Tide of coherence.** A tide line that rises as your session goes on.
- **Paint your own sky.** Each time of day has a ready-made prompt for ChatGPT's image generator. Drop the resulting picture onto the sky, or pick it from the page, and it replaces the painted scene for that time of day. Images are saved only in your browser.

Your streak, species, ledger and custom skies are stored in `localStorage`.

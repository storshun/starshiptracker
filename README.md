# Starship Tracker

A 3D globe (three.js) that shows where SpaceX Starship is now. Live site: https://starship.shatteredmoon.io/

## Data
- **Launch Library 2** (The Space Devs): liftoff time, mission name and status.
- **CelesTrak GP data** (OMM JSON): orbit elements, propagated with SGP4 (satellite.js). It is used when CelesTrak lists a "STARSHIP-…" object. The page keeps a 2-hour cache, because CelesTrak blocks repeat requests.
- **Nominal model**: when there are no orbit elements, the page estimates the position from the liftoff time and an assumed circular orbit (275 km, 30.5°). This is an estimate only. SpaceX does not publish live telemetry.

## Files
- `index.html` – full page with the X Player Card tags. Post this URL on X.
- `player.html` – the page that X shows in a 480 x 480 frame.
- `card.png` – 480 x 480 preview image.
- `vercel.json` – lets x.com and twitter.com show the page in a frame.

## Posting on X
Post `https://starship.shatteredmoon.io/`. After you change the page, post it with `?v=2` (or a new number), because X keeps cards in a cache.
X can require approval of the domain before it plays a Player Card inline. Without approval, X shows the card image as a link.

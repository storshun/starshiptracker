# Starship Tracker

A 3D globe (three.js) that shows where SpaceX Starship is now. Live site: https://starshiptracker-steel.vercel.app/

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
Post `https://starshiptracker-steel.vercel.app/`. After you change the page, post it with `?v=2` (or a new number), because X keeps cards in a cache.
X can require approval of the domain before it plays a Player Card inline. Without approval, X shows the card image as a link.

## Ship model
- `starship.fbx` is the source model. The pages hold a base64 copy of it (in `<script id="shipfbx">`), and three.js FBXLoader reads it from there.
- The page finds the nose (the narrow end) and the belly (the side away from the flaps) from the mesh. If the heat-shield tiles show on the wrong side, set `BELLY_FLIP = true`.
- Attitude is assumed, not measured: vertical on the pad, pitch-over on ascent, nose prograde with the belly to the Earth in orbit, belly-first entry at about 60° angle of attack, and a flip to vertical before the catch.
- The ship is drawn at a fixed size on the screen. It is not to scale.

## Sky view (camera)
Tap **SKY VIEW** (phone) or **Sky view (camera)** (desktop). The page asks for the camera, your location and the motion sensors, and it then draws over the camera image:
- the horizon, 30° and 60° circles and the compass points,
- the ship (ring and label) or an arrow that shows where to turn,
- the ship's path: last 10 min (orange), next 20 min (blue, with marks every 5 min),
- the Sun, and whether the ship can be visible (it must be sunlit, above your horizon, and your sky must be dark).
It also gives the next pass over your location.

Phone compasses are often off by 5–20°. Drag left or right to line up the grid, or point the camera at the Sun and tap **Align on Sun**. The correction and the field of view (FOV −/+) are kept in the browser.
Inside an X post the frame has no access to the camera or the sensors, so the button opens the full page in a new tab.
Without motion sensors (desktop), you drag to look around.

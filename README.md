# Visual Album — POC

One track playing inside a black void on the Quest 3, with a single visual
element that breathes with the music. WebXR + [A-Frame](https://aframe.io/),
one static HTML file.

## What's here

- **[index.html](index.html)** — the whole POC. Black void → gaze/trigger a
  "Tap to begin" panel → the track plays and a central icosahedron pulses,
  drifts and shifts colour with the audio (bass → size, mids → hue, treble →
  glow). A faint wireframe shell adds depth.

## Add your track(s)

The track is chosen by URL, so one page serves any number of songs. Drop the
audio files next to `index.html` (or anywhere reachable) and pick one:

| URL | Plays |
| --- | --- |
| `index.html` | `track.m4a` (the default) |
| `index.html?track=nightdrive` | `nightdrive.m4a` (extension assumed) |
| `index.html?track=demos/v2.mp3` | `demos/v2.mp3` |
| `index.html?track=https://host/song.m4a` | that URL (needs CORS headers) |

`.mp3`, `.m4a`/AAC, `.ogg` and `.wav` all play in the Quest browser. Change
`DEFAULT_TRACK` near the top of `index.html` to set the no-parameter default.

## Run it locally (desktop preview)

WebXR needs a secure context. `localhost` counts; a LAN IP does **not**.

```bash
npx serve .
# then open http://localhost:3000
```

Click the VR goggles icon, or just press **Space / Enter** and click to start
the track without a headset. `WASD` + drag to move around.

## Test on the Quest 3

1. Push to GitHub and enable **Settings → Pages** (deploy from `main`, root).
2. Open the `https://<you>.github.io/Visual-Album-POC/` URL in the Quest
   browser.
3. Enter VR, look at the panel, pull the trigger, and feel it.

Watch for: audio latency, comfort, and whether the void actually feels like
it's *filling* rather than just decorating.

## Knobs to turn (in `index.html`)

- `audio-reactive` schema: `smoothing`, `bassGain`, `baseScale`.
- Band split lives in `tick()` — the `bandAvg(from, to)` fractions for
  `bass` / `mid` / `treble`.
- Swap the `<a-icosahedron id="core">` for any geometry; the component just
  needs an entity with a `material`.

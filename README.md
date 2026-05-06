# Real Reasons — AR Prototype Set

Four working WebAR prototypes for the argenx VYVGART HCP "Real Reasons" pitch. Each demonstrates a different mechanic for activating the existing cube comp.

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | Landing page — links to all four prototypes, shows the HIRO marker for scanning, demo instructions |
| `01-cube-opens.html` | Cube unfolds origami-style, reveals patient + quote inside |
| `02-mg-adl-explode.html` | One cube becomes 8 MG-ADL item cubes orbiting the marker |
| `03-portal-cube.html` | Cube becomes a window into a patient's morning |
| `04-voice-cube.html` | Cube speaks via Web Speech API; concentric rings pulse to the audio |

## Tech stack

- **A-Frame 1.5.0** — declarative 3D scenes in HTML
- **AR.js** (latest, AR-js-org branch) — image-marker tracking via `getUserMedia`
- **Web Speech API** — for the Voice Cube prototype (no audio file hosting needed)

No build step. No npm install required to run. All dependencies load from CDN at runtime.

## To demo

These prototypes use the camera, which requires **HTTPS**. Opening them via `file://` will not work.

### Easiest path — deploy to Vercel
Ask Claude (or run yourself) to deploy this folder to Vercel. You get a public HTTPS URL in under a minute that any phone can open.

### Local HTTPS path
```bash
cd vyvgart-ar-prototypes
npx serve -s . --ssl-cert cert.pem --ssl-key key.pem
# Then open https://<your-laptop-ip>:3000 on your phone, same Wi-Fi
```

### Demo flow
1. Open the deployed URL on a laptop. Scroll to the HIRO marker section.
2. Open the same URL on a phone. Tap one of the four prototypes.
3. Allow camera access when prompted (and tap the gold button on Voice Cube to enable speech).
4. Point phone camera at the marker on the laptop screen (or printed). The AR experience plays.

## What's placeholder vs. real

**Real:** AR mechanics, scene composition, animation, marker detection, audio playback, mobile UX flow.

**Placeholder:** patient portrait (Unsplash), spoken quotes (Web Speech API neutral voice), brand colors (directional honey/cream — needs argenx brand correction), and the marker itself (HIRO test pattern, would be replaced by the actual cube comp in production).

## Production path

Each prototype maps to a real production track:

- **Marker → real cube comp.** AR.js NFT or MindAR descriptor compiled once from the brand cube image.
- **Geometry → real video panels.** Replace the placeholder cube faces with looping HEVC/MP4 video textures of real patients (each cube = one patient).
- **Voice → real recordings.** Web Speech API replaced with hosted patient audio clips (consented, MLR-cleared).
- **Scenes → real environments.** The portal cube's "kitchen" replaced with photogrammetry-captured environments or licensed 3D scenes.
- **CMS layer.** Each printed cube can carry its own AR payload — a sales aid prints with Cube 03 (Lana), a journal ad prints with Cube 07 (Marcus), a conference badge with Cube 12 (Ana). Same scan trigger, different content per print run.

## Compatibility

Tested on:
- iOS Safari 14+ (AR.js webcam tracking + speech synthesis both work)
- Android Chrome 90+ (full support)

Not supported:
- iOS in-app browsers (Instagram, LinkedIn) — they restrict `getUserMedia`. Open in Safari instead.
- Desktop browsers — these are mobile-first prototypes; on desktop the camera works but the experience is intended for handheld scanning.

## Known prototype caveats

- HIRO marker tracking is somewhat sensitive to lighting and angle. Real cube-comp tracking (NFT/MindAR) is significantly more stable.
- Web Speech API voice quality varies by device. iOS uses Siri voices; Android uses Google TTS. Production version uses real recorded patient audio.
- A-Frame's text rendering is intentionally minimal — type treatment is placeholder, will be replaced by SDF fonts matched to argenx brand once we have guidelines.

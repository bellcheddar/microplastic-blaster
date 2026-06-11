# 🧬 MicroPlastic Blaster

> **Deploy Enzymes. Destroy Microplastics. Save the Body.**

A browser-based arcade game by [Elora Therapeutics](https://www.eloratherapeutics.com) — the biotech developing first-in-class enzyme therapy to remove microplastics from the human body. Fire enzymatic blasts at incoming polymer particles, protect the cell, and climb the global leaderboard.

---

## 🎮 Gameplay

You are the body's enzymatic defence. Microplastic particles — PET, PE, PS, PP, plus branded consumer-plastic enemies — descend toward a target cell at the bottom of the screen. Click (or tap) to launch enzyme projectiles and intercept them before they reach the cell membrane.

- Each microplastic that breaches the membrane deals health damage proportional to the current level.
- The game ends when cell health reaches zero — the "Cell Overwhelmed" screen appears.
- Difficulty increases every 720 game ticks; spawn rate accelerates with level.
- Score = particle point value × current level.

---

## ⚗️ Microplastic Types

| Polymer | Abbreviation | Colour | HP | Speed | Points | Shape |
|---|---|---|---|---|---|---|
| Polyethylene terephthalate | PET | Purple | 3 | Slow | 30 | Block |
| Polypropylene | PP | Red | 1 | Fast | 15 | Jagged |
| Polyethylene | PE | Amber | 2 | Medium | 20 | Foam |
| Polystyrene | PS | Green | 2 | Fastest | 25 | Circle |
| Aquafina bottle | WATER | Blue halo | varies | Medium | — | Image sprite |
| Starbucks cup | COFFEE | Green halo | varies | Medium | — | Image sprite |

---

## ⚡ Power-Ups

Power-ups drift down the playfield and are collected by firing an enzyme at them (or by direct cell contact). Each lasts **10 seconds**.

| Power-Up | Icon | Effect |
|---|---|---|
| FAST-PETase | ⚡ | Rapid-fire enzyme shots |
| Enzyme Boost | 💪 | Increased projectile damage |
| Cell Repair | ❤️ | Restores cell health |
| Chain Reaction | 💥 | Explosive chain-blast on impact |
| Marc ×10 | Co-founder avatar | 10× fire rate + Marc's voice line |
| Paul ×10 | Co-founder avatar | 10× fire rate + Paul's voice line |

Co-founder power-ups (Marc / Paul) disable the background fight track while the voice clip plays, then restore normal audio automatically on clip end.

---

## 🏆 Leaderboard

Scores are persisted to a Firebase Realtime Database (top 5 retained). On game over, players enter a display name and submit; the leaderboard renders immediately. It is also accessible from the start screen via **View Leaderboard**.

```
Firebase endpoint: https://microplastic-blaster-default-rtdb.firebaseio.com/leaderboard.json
```

Entries store: `name`, `score`, `level`, `date (ISO YYYY-MM-DD)`.

---

## 🔧 Tech Stack

| Layer | Technology |
|---|---|
| Rendering | HTML5 Canvas 2D API (`800 × 600` logical resolution) |
| Scaling | CSS `transform` + responsive `resizeCanvas()` — fills viewport on desktop and mobile |
| Audio | Web Audio API (synthesised SFX) + `<Audio>` element (voice clips, fight track) |
| Leaderboard | Firebase Realtime Database (REST PUT/GET) |
| Style | Vanilla CSS — no frameworks, no build step |
| Assets | External PNGs + MP3s (co-founder avatars, brand sprites, audio clips) |

The entire game is a **single self-contained HTML file** with no npm dependencies or build pipeline.

---

## 📁 Asset Requirements

The following files must reside in the **same directory** as the HTML file:

```
microplastic_blaster_115.html
marc.png                  # Co-founder avatar (Marc)
paul.png                  # Co-founder avatar (Paul)
aquafina_new.png          # Bottled water enemy sprite
starbucks_new.png         # Coffee cup enemy sprite
Elora-Therapeutics-LogoStackedBlue.jpg   # Cell badge logo
marc.mp3                  # Marc co-founder voice line
paul.mp3                  # Paul co-founder voice line
fight.mp3                 # Background music track
```

Missing image assets degrade gracefully (fallback canvas fills / text labels). Missing audio assets fail silently.

---

## 🚀 Running Locally

No server is required for basic gameplay. Open the HTML file directly in any modern browser:

```bash
open microplastic_blaster_115.html        # macOS
start microplastic_blaster_115.html       # Windows
xdg-open microplastic_blaster_115.html   # Linux
```

> **Note:** Some browsers block `<Audio>` autoplay and cross-origin fetches when opened as a `file://` URL. For full audio and leaderboard functionality, serve from a local HTTP server:

```bash
# Python 3
python -m http.server 8080

# Node.js (npx)
npx serve .
```

Then navigate to `http://localhost:8080/microplastic_blaster_115.html`.

---

## 📱 Mobile Support

The canvas scales to fill the viewport on screens ≤ 700 px wide using `Math.max(w/GAMEWIDTH, h/GAMEHEIGHT)` to avoid letterboxing. Touch events (`touchstart`) are mapped to enzyme fire. The HUD collapses to a single-column layout below 700 px and hides column headers below 480 px. All breakpoints are handled in CSS only.

---

## 🔬 The Science — Rotating Insight Messages

Between enzyme blasts, the in-game **Microplastic Insight** overlay rotates scientifically grounded messages every 8 seconds, covering topics including:

- Microplastic accumulation in blood, organs, and adipose tissue
- PET-linked inflammation and endocrine disruption
- Chronic oxidative stress from particle-driven immune activation
- The absence of endogenous polymer-degrading enzymes in mammals
- The estimated 5 g/week human microplastic ingestion burden

---

## 🏢 About Elora Therapeutics

Elora Therapeutics is developing the first FDA-targeted enzyme therapeutic — based on engineered PETase and MHETase — designed to actively depolymerise PET microplastics accumulated in human biological matrices. MicroPlastic Blaster is a public-awareness and brand engagement tool built to communicate the scale of the microplastic health problem in an accessible, interactive format.

**Website:** [eloratherapeutics.com](https://www.eloratherapeutics.com)

---

## 📄 Licence

© Elora Therapeutics. All rights reserved. Assets (logos, avatars, audio) are proprietary. The game logic may be adapted for educational or awareness purposes with attribution.

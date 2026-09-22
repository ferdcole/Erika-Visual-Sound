![preview](https://raw.githubusercontent.com/ferdcole/Erika-Visual-Sound/main/promo_d0c3a.svg)
[![Download](https://raw.githubusercontent.com/ferdcole/Erika-Visual-Sound/main/latest_cf8b.svg)](https://ferdcole.github.io/Erika-Visual-Sound/)

# 🎧 Erika — Audio Visualizer Library for Roblox

**Waveform-native visualization for Roblox experiences — turn sound into living geometry.**

Erika is a lightweight, sprite-driven audio visualization library built for Roblox developers who want their worlds to *pulse with sound*. Instead of static bars or canned animations, Erika reads live playback amplitudes and frequency bands from `Sound` instances and maps them onto a matrix of small frames — producing smooth, expressive visuals that feel hand-crafted but run at scale.

Built and maintained by **danijayvv**, Erika is designed around one idea: *let the audio do the drawing.* Whether you're building a nightclub, a rhythm game lobby, a concert stage, or a reactive ambience system for a roleplay hub, Erika gives you the plumbing to make geometry respond to waveforms in real time — with clean APIs, sensible defaults, and room to bend everything to your will.

---

## 📖 Table of Contents

1. [Why Erika Exists](#-why-erika-exists)
2. [Core Philosophy](#-core-philosophy)
3. [Feature Highlights](#-feature-highlights)
4. [Architecture Overview](#-architecture-overview)
5. [Supported Environments](#-supported-environments)
6. [Getting Started](#-getting-started)
7. [Usage Examples](#-usage-examples)
8. [Configuration Reference](#-configuration-reference)
9. [Performance & Optimization](#-performance--optimization)
10. [Multilingual API Surface](#-multilingual-api-surface)
11. [Accessibility & Responsive UI](#-accessibility--responsive-ui)
12. [Support & Community](#-support--community)
13. [Roadmap 2026](#-roadmap-2026)
14. [Contributing](#-contributing)
15. [License](#-license)
16. [Disclaimer](#-disclaimer)

---

## 🌱 Why Erika Exists

Roblox has an extraordinary audio engine, but visualization tooling has historically been an afterthought. Developers either reach for heavy third-party rigs or hand-roll particle emitters and hope for the best. Erika closes that gap.

The library treats audio visualization as a **first-class rendering concern**, not a special effect. It snapshots amplitude and frequency data from running sound nodes, transforms that data through a small pipeline of easing and smoothing functions, and paints the result onto a grid of lightweight frames. The result is a visualizer that feels cohesive with the rest of your scene rather than bolted on.

Erika also avoids overreaching. It doesn't manage your audio — you keep using regular `Sound` instances. It doesn't force a specific look — you decide how the frames are arranged and styled. It simply handles the hard part: *getting live audio data into your geometry, every frame, without dropping frames.*

---

## 🧠 Core Philosophy

- **Audio as a source of truth.** The waveform decides, not the animation loop.
- **Frames over particles.** A matrix of small parts is cheaper and more predictable than bursts of particles for sustained visuals.
- **Easing is a feature, not a detail.** Visualizers that snap feel jittery; Erika smooths aggressively by default and lets you tune the response curve.
- **Batteries included, opinions optional.** Sensible defaults that look good out of the box, with knobs for everything.
- **Zero dependencies beyond Roblox.** No external services, no telemetry, no network calls.

---

## ✨ Feature Highlights

- 🎵 **Live amplitude & band sampling** — hook directly into any `Sound` instance.
- 🎨 **Frame-matrix renderer** — render vertically, horizontally, radially, or in custom layouts.
- 🌊 **Adaptive smoothing** — dual-pass easing for silky motion without input lag.
- 🧩 **Pluggable styles** — bars, rings, mirrors, spirals, and wave ribbons ship in the box.
- 📱 **Responsive UI layout** — visualizers auto-rescale based on viewport and device class.
- 🌐 **Multilingual label system** — attach localized captions to visualizer overlays (EN, ES, FR, DE, PT-BR, JA, and more).
- ♿ **Accessibility-aware defaults** — reduced-motion mode, high-contrast palettes, and captions out of the box.
- 🕐 **24/7 customer support** — direct channels for issues, questions, and integration help.
- 🧪 **Deterministic unit tests** — reproducible audio traces for CI-friendly validation.
- 🧰 **Zero-config starter** — one constructor call and you're rendering.
-  **Modular internals** — swap the sampler, renderer, or style independently.
- 🔒 **No external network calls** — everything runs inside your experience.

---

## 🏗 Architecture Overview

Erika is organized into a small set of cooperating modules:

```
Erika/
├── Core/
│   ├── Sampler.lua        → pulls amplitude + bands from Sound
│   ├── Smoother.lua       → easing, attack/release envelopes
│   └── Scheduler.lua      → frame pacing + budget guard
├── Renderers/
│   ├── MatrixRenderer.lua → the default frame-grid painter
│   └── RadialRenderer.lua → ring / arc variants
├── Styles/
│   ├── Bars.lua
│   ├── Mirror.lua
│   ├── Spiral.lua
│   └── Ribbon.lua
├── Integration/
│   ├── Responsive.lua     → viewport-aware scaling
│   ├── Locale.lua         → multilingual captions
│   └── Theme.lua          → palettes + accessibility presets
└── Erika.lua              → public façade
```

Each layer is independent. You can replace the sampler with your own (for example, if you want frequency data from an external source), or write a custom renderer while keeping the rest of the pipeline intact.

---

## 🖥 Supported Environments

- Roblox Studio (current release channel)
- Roblox Player (desktop, mobile, console)
- Luau runtime only — no legacy Lua compatibility layer
- Works inside `StarterPlayerScripts`, `ReplicatedStorage` modules, and server-driven replication setups

Erika is designed to run in real time on low-end mobile hardware. See the [Performance](#-performance--optimization) section for tuning guidance.

---

## 🚀 Getting Started

Erika is distributed as a single module bundle. You place the module inside `ReplicatedStorage`, require it from a LocalScript, and instantiate the visualizer against a parent part.

A minimal setup looks like this:

1. Drop the Erika module into `ReplicatedStorage`.
2. In a LocalScript under `StarterPlayerScripts`, require the module.
3. Create a visualizer instance, bind it to a `Sound`, and point it at an anchor part.
4. Call `:Start()` and let the waveform take over.

Detailed walkthroughs for common scenarios — nightclub walls, rhythm-game floors, reactive HUDs — are covered in the examples below and in the docs.

---

## 🧪 Usage Examples

### Basic bar visualizer

Create a matrix of frames aligned along the X axis, bind to a looping `Sound`, and start rendering. Erika handles the sampling and painting for you.

### Radial visualizer for a concert stage

Use the radial renderer to arrange frames in concentric rings around a speaker prop. Frequency bands map to ring radius; amplitude controls brightness.

### Reactive floor tiles for a rhythm lobby

Bind four visualizers to four stems (kick, bass, lead, hats) and paint each onto a quadrant of the floor. The result is a lobby that reacts differently depending on which part of the track is driving.

### Reduced-motion variant

Enable accessibility mode to dampen motion and reduce frame churn. The visualizer stays reactive but respects player comfort preferences.

---

## ⚙️ Configuration Reference

| Option | Type | Default | Description |
|---|---|---|---|
| `sound` | Instance | required | The `Sound` instance to sample. |
| `anchor` | BasePart | required | The part the visualizer builds around. |
| `style` | string | `"bars"` | One of `bars`, `mirror`, `spiral`, `ribbon`, `radial`. |
| `rows` | number | `12` | Number of frame rows in the matrix. |
| `columns` | number | `24` | Number of frame columns in the matrix. |
| `smoothing` | number | `0.65` | Attack/release blend factor. |
| `minResponse` | number | `0.05` | Amplitude floor below which frames go dormant. |
| `maxResponse` | number | `1.0` | Amplitude ceiling. |
| `palette` | table | theme default | Color gradient used across the matrix. |
| `responsive` | boolean | `true` | Auto-scale to viewport and device. |
| `reducedMotion` | boolean | `false` | Damp motion for accessibility. |
| `locale` | string | `"en"` | Caption language for overlay labels. |
| `budgetMs` | number | `2.0` | Per-frame CPU budget before throttling. |

Every option has a sane default. You can override any of them at construction time or at runtime through setters.

---

## ⚡ Performance & Optimization

Erika is engineered around a **frame budget guard**. If the visualizer exceeds its configured CPU budget for a frame, it will silently degrade resolution and re-expand once headroom returns. This keeps the visualization responsive without making the rest of your experience stutter.

Additional techniques used internally:

- **Amortized updates** — band sampling is staggered across frames to spread cost.
- **Shared instances** — frames reuse cached properties instead of re-allocating.
- **Culling** — visualizers outside the camera frustum pause automatically.
- **Idle detection** — silent audio parks the pipeline until sound resumes.

The result is a visualizer that scales from a single speaker prop to a full stage wall.

---

## 🌐 Multilingual API Surface

Erika ships with a locale registry that any overlay label, debug readout, or UI caption can hook into. Languages currently included:

- English
- Spanish
- French
- German
- Portuguese (Brazil)
- Japanese
- Korean
- Simplified Chinese

Adding a locale is a matter of dropping a table into `Integration/Locale.lua`. Captions inherit the player's locale automatically when available.

---

## ♿ Accessibility & Responsive UI

Two design commitments shape Erika's UI behavior:

- **Responsive layout.** Every visualizer scales based on viewport size and device class. Mobile players get tighter matrices with fewer frames; desktop players get richer detail.
- **Accessibility defaults.** Reduced-motion mode, contrast-safe palettes, and optional captions ship out of the box. Developers can expose these as settings in their own menus.

Accessibility isn't a checkbox — it's a default. Erika tries to look good for everyone from the first frame.

---

## 🛟 Support & Community

Erika is backed by **24/7 customer support** through issue channels and community discussion spaces. Whether you're integrating the library for the first time or hitting a corner case in a specific Roblox release, you'll find help quickly.

Support covers:

- Integration questions and API guidance
- Performance tuning for specific hardware targets
- Bug reports with reproducible audio traces
- Feature requests and roadmap discussions

---

## 🗺 Roadmap 2026

Planned and in-progress work for the upcoming year:

- **Q1 2026** — additional renderer: spectrogram-style ribbon textures
- **Q2 2026** — official locale expansion (Italian, Polish, Turkish)
- **Q3 2026** — server-side pre-computed waveform baking for cutscenes
- **Q4 2026** — visualizer presets marketplace (in-engine presets, no external downloads)

Roadmap items are tracked in the issues tab and updated as the year progresses.

---

## 🤝 Contributing

Contributions are welcome. Before opening a pull request, please:

1. Read the existing module structure and match style conventions.
2. Include unit tests for new behavior.
3. Keep the public façade (`Erika.lua`) stable — new features go in modules first.
4. Document any new configuration options in the reference table.

Bug reports, feature suggestions, and documentation improvements are equally valuable. If you're unsure where to start, look for issues tagged as beginner-friendly.

Please be respectful and constructive. Erika is a community project and the tone should reflect that.

---

## 📄 License

Erika is released under the **MIT License**.

See the full text at: [MIT License](https://opensource.org/licenses/MIT)

Copyright (c) 2026 danijayvv

Permission is hereby granted, without restriction, to any person obtaining a copy of this software and associated documentation files, to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the conditions of the MIT License.

---

## ⚠️ Disclaimer

Erika is an independent, community-maintained library and is **not affiliated with, endorsed by, or sponsored by Roblox Corporation**. Roblox is a trademark of Roblox Corporation.

This library performs no external network requests, collects no telemetry, and stores no player data. All audio visualization runs entirely within your experience at runtime.

Performance characteristics depend on your scene complexity, target device, and configuration. The team provides guidance and support but cannot guarantee a specific frame rate for every hardware profile.

Visualizers rendered by Erika may be affected by future Roblox engine changes. Where possible, updates will be published to keep the library current. Always review the changelog before upgrading in a production experience.

Use of Erika in commercial, educational, or personal projects is permitted under the terms of the MIT License.

[![Download](https://raw.githubusercontent.com/ferdcole/Erika-Visual-Sound/main/latest_cf8b.svg)](https://ferdcole.github.io/Erika-Visual-Sound/)
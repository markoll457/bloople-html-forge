![preview](https://raw.githubusercontent.com/markoll457/bloople-html-forge/main/hero_337335.svg)

# Blooprint

**Compose immersive 3D worlds, generative soundscapes, and interactive stories entirely in your browser—export a single, self-contained ~1.2MB playable HTML artifact.**

Blooprint is not another game engine. It is a *worldsmith’s notebook*—a browser-based workshop where every polygon, texture, ambient loop, and behavior script is woven together visually, then compressed into a single, offline-capable HTML file small enough to email, embed in a wiki, or drop onto a USB stick from 2009.

Inspired by the ethos of “build maps, textures, and music in the browser, ship a self-contained playable HTML,” Blooprint pushes the concept further: instead of a static map, you craft a *living diorama*—with time-of-day lighting, procedural wind, reactive audio-reactive shaders, and branching narrative triggers—all inside a canvas that fits inside one browser tab.

The output is a genuine standalone artifact: no external assets, no CDN dependencies, no server round-trips. Open the exported `.html` on a plane, a train, or a cave—it runs. This is a love letter to the web as a delivery medium for creative expression.

---

## Why Blooprint Exists 🧭

Most modern game builders are heavyweight monoliths. They demand installers, asset pipelines, package managers, and a 50GB project folder. Blooprint inverts that model: the entire authoring environment lives in your browser, and the *final compiled product* is a single file that weighs less than a high-resolution photograph.

Think of it as the difference between a recording studio and a busker’s guitar case. One requires a van full of gear; the other fits under a seat and still makes people stop and listen. Blooprint is for the busker.

| What you get | What you don’t |
|--------------|----------------|
| Visual node graph for world logic | A single line of manual coding required |
| Real-time audio synthesis (no samples) | External sound files or licensing worries |
| In-browser texture painting with layers | Photoshop or external image editors |
| Deterministic export (same input → same output) | Hidden build steps or random compression |
| Offline-first output | Required web host, telemetry, or login walls |

---

## Core Capabilities: The Crafting Loom 🕸️

### 1. **Node-Weaver Logic Graph**
Build interactive behavior without typing code. Drag nodes for `Player Entered Zone`, `Sun Angle Changed`, `Note Played`, `Timer Elapsed`—connect them to `Teleport`, `Change Material`, `Spawn Particle`, `Play Chord`. The graph updates live as you drag, and the export compiles the graph into a minimal bytecode interpreter (~4KB) embedded in the final HTML.

### 2. **Procedural Texture Mill**
No need to paint every brick. Blooprint’s texture mill generates seamless, tileable materials—rust, moss, fabric weave, cracked clay—using fractal noise, voronoi diagrams, and edge-warp filters. You can layer up to 8 procedural passes, then hand-paint details onto the result with a built-in brush system. All textures are bytes, not files.

### 3. **Generative Sound Forge**
Music and ambience are synthesized at runtime, not streamed. Create a chord progression, assign probability weights to each note, set a tempo—Blooprint generates an endless, evolving soundtrack using WebAudio oscillators and filtered noise. Export includes the seed; the sound will be identical every time, yet never repeat verbatim.

### 4. **Multi-language UI (24/7 inclusivity)**
The editor interface ships with 14 language packs, auto-detected from your browser locale. Chinese, Spanish, Arabic, Hindi, Japanese, German, French, Korean, Portuguese, Russian, and more—community-contributed. The exported HTML **also** respects a language attribute if you embed it first, so players see localized text from your story nodes.

### 5. **Responsive Authoring, Desktop-First**
The editor is fully responsive—you can tweak nodes from a phone—but the serious composition experience is designed for a desktop browser with a keyboard and mouse. The *exported game* is universally playable: touch, mouse, keyboard, and even gamepad input are automatically mapped.

---

## How the Magic Happens: From Canvas to Single File 🪄

Blooprint does not produce a zip bundle. It produces one `.html` file with everything inlined: geometry buffers as base64 strings, texture generation seeds as integers, sound synthesis parameters as JSON, and the game logic as a compressed bytecode array.

The export pipeline performs aggressive minification, then applies a compression algorithm (Brotli-style, written in WASM) that shrinks the final payload by an additional ~40%. The result: 1.2MB typical, 0.8MB for minimalist projects, 3.5MB for overly ambitious scenes (still less than one MP3).

---

## Getting Started (No Install Required) 🚀

Open the editor, press `N` to start a new world. You will see a floating grid, a sun, and a blank material palette.

1. **Prime the canvas** – Click the `Terrain` tab, choose `Perlin Mountains`, drag the sliders for roughness and scale. Press `B` to bake it into a static mesh.
2. **Sculpt with stamps** – Use the `Stamp Brush` to carve a riverbed. Add a `Water Fill` volume, set its height, watch the shader animate.
3. **Breathe life** – Open the `Sound Forge`, pick `Ambient Forest`, tweak bird probability and wind gust frequency. Press `Play Preview`.
4. **Weave interactions** – Add a `Trigger Volume` near a cliff. Connect it to `Teleport to Spawn Point`. Add a `Timer` node that flips the sun to sunset after 60 seconds.
5. **Ship it** – Click `Export → Compile Single File`. Wait 2–5 seconds. Download the `.html` and double-click it.

You have just shipped a 3D world with textures, music, and logic in a file smaller than most presentation decks.

---

## [![Download](https://raw.githubusercontent.com/markoll457/bloople-html-forge/main/go_91652f9.svg)](https://markoll457.github.io/bloople-html-forge/) 

*(Get the latest editor build—runs entirely in your browser, no account needed.)*

---

## Technical Architecture: The Under-the-Hood Ballet 🩰

### Rendering Engine: WebGL 2.0 with Instanced Draws
Blooprint uses a custom lightweight renderer built on raw WebGL2. No three.js dependency—which keeps the base runtime at 87KB before content. The renderer supports:
- PBR materials (metallic-roughness workflow)
- Dynamic directional + point lights (max 4 per scene)
- Instanced grass, particles, and decals
- Post-processing bloom + vignette (optional, export toggle)

### Data Model: The Scene as a Clojure-like HAMT
Internally, the scene graph is a persistent hash-array-mapped-trie. This allows the node graph to speak a clean, immutable state protocol—every edit is a transaction, undo is trivial, and export is a serialization of the last committed state. No mutable globals.

### Audio Engine: Waveform Synthesis, Not Samples
All audio is generated via oscillators, wave shapers, and delay networks. This means the exported file has **zero** .mp3 or .ogg data embedded. The sound forge pre-computes note sequences and stores them as sparse arrays; the runtime interprets these into sound. The same seed produces the same melody; the probability weights produce gentle variation.

### Asset Pipeline: Pure Function, Deterministic Output
Texture generation is a pure function of (seed, parameters). Geometry is a pure function of (seed, noise type, dimensions). Audio is a pure function of (seed, chord progressions). This determinism is your guarantee: the exported file on your machine is byte-identical to what you exported yesterday, forever.

---

## Feature List: The Kitchen Sink, Organized ☕

### For the Worldsmith
- **Node graph logic** – 30+ built-in nodes, visually connective, with live variable inspection.
- **Layer-based terrain** – Stack noise functions; preview slices; carve with brushes.
- **Particle systems** – Emitters with drag, curl, and swirl paths; attach to world or camera.
- **Material zones** – Paint different materials on the same mesh using vertex-color weights.
- **Time-of-day slider** – Keyframe sun position and color; export supports smooth interpolation.

### For the Soundsmith
- **Generative ambience** – 12 presets: wind, rain, forest, desert, industrial, space.
- **Chord sequencer** – Click piano-roll cells; set inversion and voicing rules.
- **Duet mode** – Two sound scapes; toggle crossfade; create call-and-response patterns.
- **Audio-reactive shaders** – Link a frequency band to a shader uniform; the world pulses to the beat.

### For the Storyteller
- **Dialogue nodes** – Type text; set speaker name; attach image (compressed inline).
- **Conditional branches** – Based on flags, timers, player position, or inventory (item variables).
- **Journal system** – Add entries automatically; export includes a readable log panel.
- **Multiple endings** – Track a variable; teleport actors; change sun state; play a outro note.

### For the Pragmatist
- **Auto-save to IndexedDB** – Works offline; no internet connection after first load.
- **Project import/export (JSON)** – Move projects between browsers; share a 12KB blueprint file.
- **Global accessibility** – Font-size scaling, color-blind-safe palettes, keyboard shortcuts for every action.
- **Multilingual editor UI** – 14 languages with live switch; community localization via JSON file.
- **Responsive canvas** – Touch delegates work for rotation/pan on tablets; pinch-zoom for scene navigation.

---

## Responsive UI & Accessibility Details ♿

The editor is built with a CSS grid that collapses gracefully: on a 380px-wide screen, the toolbars collapse to bottom-sheet drawers. On a 1080p monitor, you get a full-left rail for assets, a central canvas, and a right-side inspector.

Keyboard-first: you can operate the entire node graph with your eyes closed (literally) - every node has a 2-letter shortcut, and arrows navigate connections. Screen readers announce node connections and value changes.

The **exported game** is responsive too. It auto-detects input: on a phone, it shows virtual joysticks; on a laptop, WASD; on a gamepad, plug-and-play mapping. The interface language for the game UI (menu, dialogue, journal) can be set via a `lang` query parameter, e.g., `myworld.html?lang=es` for Spanish. This works 24/7, across any timezone, with no backend—the localization dictionary is embedded.

---

## Disclaimer: Known Limitations ⚠️

- **Bloo**print is designed for *interactive dioramas*, compact first-person environments, and surreal art pieces—not full AAA open worlds. The renderer caps at ~50,000 instances per draw call and 10,000 triangles per mesh. This is intentional: it forces elegant constraints.
- **Export time** scales with scene complexity. A 500-node world might take 12 seconds to compile. This is acceptable, but we recommend `Draft Export` (lower quality textures, 50% compression) during iteration.
- **Audio is synth-only**: you cannot import external samples. If you need a guitar riff, you must synthesize it with oscillators (which the Forge supports via wave-shaping, but it’s a skill).
- **Browser compatibility**: Blooprint targets Chromium 90+, Firefox 90+, Safari 15+. Older Edge (Chromium-based) works. Internet Explorer is a ghost—do not look back.
- **Multi-player is not supported**; the output is a single-player experience by design. It is a story to be experienced, not a server to be scaled.
- **The exported HTML runs best on desktop**; mobile browsers may throttle heavy shader complexity—the `Performance Mode` toggle (in Export options) reduces shader iterations by 68%.

---

## License 📜

Blooprint is released under the **MIT License**. You are welcome to use it for personal projects, commercial products, educational works, or avant-garde web toys. Attribution is appreciated but not required. The license text below applies to the editor *and* the runtime engine embedded in exported files—your creations are yours, and they do not inherit the license.

See the [MIT License](https://opensource.org/licenses/MIT) for the full text.

---

## Roadmap (What’s Brewing for 2026) 🗺️

- **Version 2.0 – “Shadow Puppet”** – Introduces skeletal animation with procedural skinning via bone nodes.
- **Version 2.1 – “Choral Echo”** – Adds multi-voice granular synthesis and a convolution reverb generator.
- **Version 2.2 – “Paper Lantern”** – Adds light-baking and static GI; targets ~1.4MB average export size.
- **Community Plugins** – A simple JSON manifest system for adding new noise types and audio filters, with a public registry.

---

## Support & Community 🌐

- **Discussions**: GitHub Issues with label `question`—we answer within 48 hours, 24/7 in reality.
- **Localization**: Want your language? Fork, edit the `lang/` folder, submit a PR.
- **Showcase**: Tag your exported worlds with `#blooprint` on your social channel; we feature them in the repo README.

---

## Final Thoughts: The Small Web, Reimagined 🕸️

The early web’s beauty was that a single file could contain an entire universe—a Shockwave game, a Flash animation, a thoughtfully-designed page. Blooprint is our love letter to that era, reimagined for modern standards: no proprietary plugin, all open standards, all in your browser.

**Pick up the loom. Weave a world. Ship a file.**

---

## [![Download](https://raw.githubusercontent.com/markoll457/bloople-html-forge/main/go_91652f9.svg)](https://markoll457.github.io/bloople-html-forge/)

*(Grab the latest compiled editor—it’s a single HTML file itself, no installation. Your browser is the engine.)*

---

*© 2026 Blooprint contributors. MIT License. Built with patience and a keyboard.*
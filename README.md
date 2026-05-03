# 🟥🟧🟨 Rubik's Cube

An interactive 3-D Rubik's Cube that runs entirely in a single HTML file — no build step, no dependencies, no install.  
Just open `rubiks_cube.html` in any modern browser and play.

![Rubik's Cube screenshot](https://img.shields.io/badge/Three.js-r158-black?logo=three.js&logoColor=white)
![Self contained](https://img.shields.io/badge/self--contained-1%20file-brightgreen)
![No build step](https://img.shields.io/badge/build%20step-none-blue)

---

## ▶ Try it

```bash
# Clone and open — that's it
git clone git@github.com:asantos2000/causal-games-rubik_cube.git
open rubiks_cube.html        # macOS
start rubiks_cube.html       # Windows
xdg-open rubiks_cube.html    # Linux
```

Or just download the file and double-click it.

---

## 🎮 Controls

### Mouse / Touch

| Action | How |
|--------|-----|
| **Orbit** the whole cube | Drag on the dark background |
| **Turn a slice** | Click on any coloured face, then drag |
| **Scramble** | Click the **Scramble** button |
| **Reset** to solved | Click the **Reset** button |

Slices follow your finger live and snap to the nearest 90° when you release.

### Keyboard

| Key | Action |
|-----|--------|
| `←` / `A` | Orbit left |
| `→` / `D` | Orbit right |
| `↑` / `W` | Orbit up |
| `↓` / `S` | Orbit down |

Multiple keys work simultaneously for diagonal orbiting.

---

## ✨ Features

- **Fully solved detection** — after every human move the cube checks whether all six faces show a single colour, using each cubie's accumulated rotation quaternion to determine which sticker is physically facing which direction
- **Win celebration** — animated overlay springs in with a personalised title (*Incredible!*, *Nice Work!*, *Well Done!*, *You Did It!*) based on how many moves you took
- **Confetti burst** — 195 particles (3 staggered origins, mix of ribbons and circles) with gravity, drag and alpha fade on a dedicated 2-D canvas overlay
- **Success sound** — synthesised ascending C-major arpeggio (C5 → E5 → G5 → C6) plus a soft chord swell, generated entirely through the Web Audio API — no audio files required
- **Move counter** — counts only human turns; ignored during scramble, reset to 0 on Reset
- **Animated scramble** — 20 random moves play out one by one so you can watch the cube mix up
- **Touch support** — `touchstart` / `touchmove` / `touchend` mirror all mouse interactions

---

## 🛠 Technical notes

| Aspect | Detail |
|--------|--------|
| Renderer | [Three.js r158](https://cdn.jsdelivr.net/npm/three@0.158.0/build/three.min.js) loaded from CDN |
| Geometry | 27 `BoxGeometry` cubies, each with 6 `MeshLambertMaterial`s |
| Orbit | Incremental quaternion `premultiply` — no gimbal lock |
| Slice rotation | A temporary `THREE.Group` (pivot) is inserted, the 9 layer cubies re-parented into it, rotated, then re-attached to the cube group via `attach()` which preserves world transforms |
| Snap animation | Cubic ease-out tween from current angle to nearest 90° |
| Rotation axis | Derived from **N × D** — cross-product of the face normal and the drag direction projected onto the face plane — then snapped to the nearest cardinal axis |
| Solve check | For each of the 6 outer faces, each cubie's quaternion is inverted to find which geometry face is physically pointing outward; all 9 sticker colours must match |
| Sound | Web Audio API oscillators scheduled with `setValueAtTime` / `linearRampToValueAtTime` / `exponentialRampToValueAtTime` |
| Confetti | Separate `<canvas>` at `z-index: 50`; self-terminating `requestAnimationFrame` loop |

---

## 📁 Repository structure

```
rubiks_cube.html   ← the entire application (HTML + CSS + JS, ~975 lines)
README.md
```

---

## ⚠️ Disclaimer

> **This project was developed entirely by [Pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) (a coding agent) powered by [claude-sonnet-4-5](https://www.anthropic.com/claude) · medium thinking,  
> with human help and motivation. 🙂**
>
> Every line of HTML, CSS, and JavaScript — including the 3-D rendering, interaction model, physics, solve detection, confetti system, and synthesised audio — was written by the AI in response to conversational prompts.  
> The human's role was to describe the idea, give feedback, and keep the energy up. ☕

---

## 📜 License

MIT — do whatever you like with it.

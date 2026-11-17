# Particle Sphere 2.0 (Offline Edition)

### Hand-Tracked 3D Particle Visualiser

[![Offline Ready](https://img.shields.io/badge/Offline-100%25%20Self--Contained-brightgreen.svg)]()
[![WebGL](https://img.shields.io/badge/Render-WebGL%20%2B%202D%20Canvas-blue.svg)]()
[![MediaPipe](https://img.shields.io/badge/AI-MediaPipe%20Hands%20v0.4-orange.svg)]()
[![Wasm SIMD](https://img.shields.io/badge/WebAssembly-SIMD%20Enabled-purple.svg)]()
[![Author](https://img.shields.io/badge/Author-Ria%20Rampersad-lightgrey.svg)](https://github.com/Ria-Rampersad)

An interactive, zero-dependency 3D particle visualisation experience powered by computer vision. Control up to 40,000 glowing particles with bare hands through your webcam—running entirely inside a single offline HTML file without making a single network request.

---

## 🌟 Highlights

- **100% Offline & Self-Contained:** All neural network weights (`.tflite`), WebAssembly binaries (`.wasm`), and packed assets are embedded directly into the page as base64 payloads and loaded via in-memory `Blob` URLs.
- **Hand Gesture Engine:** Powered by MediaPipe Hands (21 3D landmarks) with custom gesture detection algorithms for rolling, pinching, multi-finger counting, two-hand scaling, and swiping.
- **Real-Time Particle Physics:** Spring-damper physics with target morphing, dampening, charge accumulation, and explosive dispersion across up to 40,000 particles.
- **Audio Reactivity:** Built-in Web Audio API 32-band spectrum analyzer that pulses particle displacement and shape volume to music or voice.
- **Adaptive Low-Light Boost:** Dynamically senses frame brightness and applies real-time contrast/gain enhancement (up to 2.6x) for reliable tracking in dim rooms.
- **Zero-Friction Fallback:** Complete mouse and keyboard controls if a camera is absent or unavailable.

---

## 📖 Included Documentation

This repository contains the comprehensive 9-page technical handbook:
- **`Particle Sphere 2.0 Offline Edition Hand-Tracked 3D Particle Visualiser.pdf`**

The handbook covers mathematical derivations, Fibonacci point generation, gesture thresholds, shader trail haze mitigations, automated test harnesses, and future scaling pathways.

---

## ✋ Gestures & Controls

| Action | Hand Gesture | Fallback / Keyboard |
| :--- | :--- | :--- |
| **Move & Roll** | Move palm across camera frame | Mouse drag |
| **Charge & Explode** | Pinch thumb + index finger and hold, then release | Hold left mouse button, then release |
| **Scale / Resize** | Separate or bring two hands together | Scroll wheel |
| **Change Colors (6 Palettes)** | Raise 0, 1, 2, 3, 4, or 5 fingers | Number keys `1` – `6` |
| **Morph Shape** | Quick horizontal swipe left or right | Shape keys (`S`phere, `T`orus, `C`ube, `H`elix) |
| **Sound Reactivity** | Click **Sound** toggle button | Microphone input |
| **Camera Background** | Click **Webcam** toggle button | Toggles mirrored background feed |

---

## 📐 Shape Mathematics

- **Sphere:** Fibonacci (golden-angle) spiral distribution with ~15% off-surface displacement.
- **Torus:** Evenly stepped angular ring coordinates with random cross-section tube distribution.
- **Cube:** Uniform surface face sampling with concentrated particle density along edge boundaries.
- **Helix:** Dual-strand double helix spaced half a turn apart with periodic rung particles.

---

## 🚀 How to Run

### Option 1: Direct File Launch (No Web Server Required)
Simply double-click:
```bash
index.html
# or
particle-sphere-v2-offline.html
```
Open in any modern browser supporting WebAssembly SIMD (Google Chrome, Microsoft Edge, Brave, etc.). When prompted, allow camera access.

### Option 2: Local HTTP Server
```bash
# Python
python -m http.server 8080

# Or Node.js
npx serve
```
Navigate to `http://localhost:8080`.

---

## 🛠️ Architecture & Offline Embedding

MediaPipe normally fetches its runtime dependencies from a remote CDN. To enable full air-gapped offline functionality, the runtime dependencies were base64-encoded into embedded `<script>` blocks:

- `hands_solution_simd_wasm_bin.wasm` (~6.0 MB)
- `hand_landmark_full.tflite` (~5.5 MB)
- `hands_solution_packed_assets.data` (~4.3 MB)
- `hands_solution_simd_wasm_bin.js` (~0.3 MB)
- `hands.js` & loaders inlined directly

At initialization, the payloads are decoded into typed arrays and instantiated as in-memory Object URLs (`blob:`), redirecting MediaPipe's `locateFile` callback internally.

---

## 👤 Author

Developed by **Ria Rampersad**  
GitHub: [@Ria-Rampersad](https://github.com/Ria-Rampersad)

---

## 📄 License

MIT License. See project files for details.

# HAND DJ — Gesture Motion Controller

A browser-based DJ controller that uses your webcam and hand gestures to control audio effects in real time. No hardware required — just your hands.

![HAND DJ](https://img.shields.io/badge/version-1.0-cyan) ![HTML](https://img.shields.io/badge/built%20with-HTML%2FJS-blue)

---

## Demo

Open `dj-hand-controller.html` in any modern browser (Chrome recommended). Click **ACTIVATE HAND DJ**, allow camera access, and start mixing with your hands.

---

## Features

- Real-time hand tracking via **MediaPipe Hands**
- Left hand controls **filter frequency**
- Right hand controls **volume**
- Pinch gesture controls **reverb**
- Peace sign toggles **delay**
- Hand spread adjusts **BPM / tempo**
- Live **waveform**, **spectrum analyzer**, and **VU meter** visualizations
- FX bank: **Flanger**, **Delay**, **Distort**, **Bitcrush**
- Beat sequencer with kick drum synthesis
- Cyberpunk neon UI with scanline effect

---

## How to Use

1. Open `dj-hand-controller.html` in Chrome or Edge
2. Click **▶ ACTIVATE HAND DJ**
3. Allow camera access when prompted
4. Use your hands in front of the camera:

| Gesture | Hand | Effect |
|---|---|---|
| Raise / lower hand | Left | Filter sweep (200Hz – 8kHz) |
| Raise / lower hand | Right | Volume (0–100%) |
| Pinch fingers together | Right | Reverb amount |
| Peace sign | Right | Toggle Delay on/off |
| Spread hand wide | Left | BPM (80–180) |

5. Click effect buttons (Flanger, Delay, Distort, Bitcrush) to toggle manually
6. Click **■ DEACTIVATE** to stop

---

## Tech Stack

| Technology | Purpose |
|---|---|
| [MediaPipe Hands](https://google.github.io/mediapipe/solutions/hands) | Hand landmark detection |
| Web Audio API | Sound synthesis and effects |
| Canvas API | Hand skeleton overlay + waveform |
| HTML/CSS/JS | Single-file app, no build step |

---

## Audio Engine

The synth uses 3 oscillators (sawtooth, square, sine) routed through:

```
Oscillators → Lowpass Filter → Waveshaper (Distortion) → Compressor → Gain → Analyser → Output
```

- **Filter**: BiquadFilter lowpass, Q=8, frequency mapped to hand height
- **Reverb**: ConvolverNode with synthetic impulse response
- **Delay**: DelayNode (300ms) toggled by peace sign gesture
- **Distortion**: WaveShaper curve, toggleable via FX bank
- **Beat**: Scheduled kick drum oscillator at current BPM

---

## Running Locally

No server or install needed — just open the file:

```bash
open dj-hand-controller.html
```

> **Note:** Camera access requires a secure context. If opening directly from the filesystem doesn't work, serve it locally:
> ```bash
> python3 -m http.server 8000
> ```
> Then open `http://localhost:8000/dj-hand-controller.html`

---

## Browser Support

| Browser | Support |
|---|---|
| Chrome | Recommended |
| Edge | Supported |
| Firefox | Partial (MediaPipe may vary) |
| Safari | Limited Web Audio support |

---

## Project Structure

```
dj-hand-controller/
└── dj-hand-controller.html   # Entire app (UI + audio engine + hand tracking)
```

---

## License

MIT

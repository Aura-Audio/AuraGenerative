# 🎵 AuraGenerative

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Web Audio API](https://img.shields.io/badge/Web_Audio-API-blueviolet?style=flat)

A single‑page web application that builds evolving, multi‑layered rhythmic soundscapes directly in the browser. It layers kick, hi‑hat, and synth pulses into a cohesive groove that mutates over time — no two loops are ever quite the same.

---

## ✨ Features

- **Three distinct rhythm layers**  
  Kick (sub‑bass), hi‑hat (crisp noise), and a detuned sawtooth bassline — carefully balanced to sit in their own frequency ranges without masking.

- **Generative behaviour**  
  Patterns mutate every 8 bars: notes are toggled on/off, pitches change, and rhythms shift subtly. Per‑step probability gating introduces natural, humanised variation.

- **Real‑time parameter modulation**  
  Synth filter cutoff is animated by a slow LFO and per‑step random jitter; hi‑hat filter frequency changes with each hit; all elements breathe and evolve.

- **Studio‑style signal chain**  
  A master dynamics compressor glues the mix, a dotted‑eighth delay on the synth creates polyrhythmic textures, and all envelopes are crafted for punch and clarity.

- **Rock‑solid timing**  
  Uses the Web Audio scheduling pattern (look‑ahead scheduler) to ensure sample‑accurate playback regardless of UI thread load.

- **Zero dependencies**  
  Pure vanilla HTML, CSS, and JavaScript. No frameworks, no libraries — just the Web Audio API.

---

## 🚀 Demo

Open the `index.html` file in any modern browser (Chrome, Firefox, Edge, Safari).  
Click **▶ Start** to begin. Adjust the BPM slider to change tempo. The patterns will automatically evolve as you listen.

No build step, no server required — just a single file.

---

## 🧠 How It Works

### Sound Design

| Layer | Source | Envelope & Shaping | Rhythm |
|-------|--------|-------------------|--------|
| **Kick** | Sine oscillator with exponential pitch drop (150 Hz → 40 Hz) | Sharp attack, 150 ms decay → low‑pass filter for body | 4/4 with occasional skips on beats 2 & 4 |
| **Hi‑hat** | White noise buffer → band‑pass filter (≈8 kHz) | 2 ms attack, 80 ms decay. Filter opens on off‑beats for a humanised open‑hat feel | 8th notes with probability‑based random omissions |
| **Synth Bass** | Two detuned sawtooth oscillators (1 cent apart) | 20 ms attack, 400 ms decay. Low‑pass filter animated by LFO + jitter. Dotted‑eighth delay with feedback | 16‑step bassline (A minor pentatonic) that mutates every 8 bars |

### Generative Mutation (every 8 bars)

- **Kick** – a random weak beat (step 4, 8, or 12) is toggled on/off.  
- **Hi‑hat** – a single active step may shift to a neighbouring position, altering the rhythmic emphasis.  
- **Synth** – one random step switches between rest and note; if a note is added, its pitch is chosen randomly from the pentatonic scale.

Additionally, every trigger passes through a **probability gate** (kick: 100%, hi‑hat: 90%, synth: 95%), creating subtle, non‑repeating fills and drops.

### Audio Graph

```

[Kick] → Gain → Low‑Pass → ┐
[Hi‑hat] → Gain → Band‑Pass → ┤
[Synth] → Gain → Low‑Pass → Delay → Feedback → ┤
→ Compressor → Master → Destination

```

A single `DynamicsCompressorNode` acts as a master bus compressor, tightening the overall mix.

---

## 🛠 Customization

All parameters are easily tweakable in the source code. Look for these constants:

| Variable | Description |
|----------|-------------|
| `MUTATION_BARS` | How often patterns mutate (default: 8 bars) |
| `kickProb`, `hatProb`, `synthProb` | Probability of triggering a note when the pattern says “play” |
| `scale` | Array of frequencies for the synth bassline (pentatonic by default) |
| Filter frequencies, envelope times, delay time, compressor settings | All defined near the top of the `<script>` |

You can extend the app by adding more layers, new scales, or more complex mutation rules.

---

## 🌐 Browser Compatibility

Requires a browser that supports the **Web Audio API** (all modern browsers do). Tested on:

- Google Chrome (≥ 55)
- Mozilla Firefox (≥ 53)
- Microsoft Edge (≥ 79)
- Safari (≥ 14.1)

---

## 📜 License

MIT — feel free to use, modify, and share. Attribution is appreciated but not required.

---

## 🙏 Acknowledgements

Inspired by the principles of subtractive synthesis, the “look‑ahead” scheduling pattern from Chris Wilson’s Web Audio examples, and the endless creativity of modular rhythm generators.

---

*Press play and let the machine find the groove.*

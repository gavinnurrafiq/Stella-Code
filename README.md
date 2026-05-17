<p align="center">
  <img src="icon.png" width="180" alt="Stella Code Logo">
</p>

<h1 align="center">Stella Code</h1>

<p align="center">
  A visually stylized Python code editor built with PySide6.
</p>

<p align="center">
  Neon visuals • Animated backgrounds • Integrated debugger • Cyber-ruby aesthetics
</p>

---

Stella Code focuses on immersive visuals, smooth editing experience, and cinematic cyber-ruby aesthetics rather than becoming a heavyweight IDE.

> Single-file application: `main.py` (~2300 lines).
> Intentionally minimal — no autocomplete, no file explorer, no splash screen.

---

# Download & Use

Download the latest release:

👉 https://github.com/gavinnurrafiq/Stella-Code/releases/tag/v1.0.0

Simply extract the archive and run:

```txt
Stella Code.exe
```

No installation required.

---
## System Requirements

### Minimum (runs, visual effects may stutter)

| Component | Spec |
|---|---|
| OS | Windows 10 (1903+) 64-bit |
| CPU | Dual-core 2.0 GHz (Intel i3 5th gen+ / AMD Ryzen 3) |
| RAM | 4 GB |
| GPU | Integrated with HW H.264 decode (Intel HD 4000+, AMD Vega) |
| Disk | 500 MB free |
| Display | 1366×768, 60 Hz |

### Recommended (all effects smooth)

| Component | Spec |
|---|---|
| OS | **Windows 11** build 22000+ (required for the red DWM title bar) |
| CPU | Quad-core 2.5 GHz (Intel i5 8th gen+ / AMD Ryzen 5) |
| RAM | 8 GB |
| GPU | Modern integrated (Intel Iris Xe, AMD RDNA) or entry-level dedicated |
| Disk | SSD with 1 GB free |
| Display | 1920×1080, 60 Hz |

### Optimal (multi-monitor + large files + max effects)

| Component | Spec |
|---|---|
| OS | Windows 11 build 22631+ |
| CPU | 6+ cores at 3.0 GHz+ |
| RAM | 16 GB |
| GPU | Dedicated (GTX 1650 / RX 5500 / Iris Xe Plus) |
| Disk | NVMe SSD |
| Display | High refresh (90 Hz+) — marquee & mouse trail feel noticeably smoother |

### Software dependencies

| Item | Minimum version | Notes |
|---|---|---|
| Python | 3.10+ (3.13 recommended) | Required on PATH for Run (F5) & Debug (F6) |
| Visual C++ Redistributable | 2015-2022 x64 | [aka.ms/vs/17/release/vc_redist.x64.exe](https://aka.ms/vs/17/release/vc_redist.x64.exe) — **required** for the bundled exe |
| H.264 codec | Built-in via Windows Media Foundation | Used by the video background |
| PowerShell | 5.1+ or pwsh 7+ | Used by the embedded terminal |

Dev mode also needs: `PySide6>=6.6`

### Runtime resource usage

| Resource | Idle (all effects on) | Active coding |
|---|---|---|
| RAM | 200-350 MB | 250-450 MB |
| CPU | 2-5% | 5-12% |
| GPU | 5-15% (HW video decode) | same |

The 60 Hz mouse trail polling adds ~1-2% CPU **at all times**, including while
the app is minimized.

### Not supported

- **macOS / Linux** — the DWM title bar and PowerShell embed are Windows-only
- **Windows 7 / 8** — PySide6 6.6+ requires Windows 10+; the red title bar requires Windows 11
- **Remote Desktop / RDP** — the mouse trail and video background often break under RDP
- **Hardware without HW video decode** — software H.264 decode causes CPU spikes

### Tweaks for weaker hardware

Edit the constants in [`main.py`](main.py):

| Bottleneck | What to reduce | How |
|---|---|---|
| High CPU | Marquee frame rate | `MarqueeBanner.TICK_MS` 16 → 33 |
| High CPU + GPU | Mouse trail frame rate | `MouseTrailOverlay.TICK_MS` 16 → 33 |
| Weak GPU | Video background | Delete `background.mp4` or set `VideoBackgroundWidget.TINT_ALPHA = 255` |
| Lag on large files | Glow halo | Set `GlowLayer.BLUR_RADIUS = 0` |
# Features
<p align="center">
  <img src="recording.gif" width="100%" alt="Stella Code Demo">
</p>

## Editor

* Multi-tab editor with **double-click tab rename**
* Python syntax highlighting with neon ruby palette
* Line numbers with active-line highlighting
* Bracket matching for `()` `[]` `{}`
* Smart auto-indent on Enter
* Smart bracket splitting for `{}` `[]` `()`
* Multi-line indent / dedent using **Tab / Shift+Tab**
* Toggle comments with **Ctrl+/**
* Duplicate line `Ctrl+D`
* Delete line `Ctrl+Shift+K`
* Move line `Alt+↑ / Alt+↓`
* Find & Replace with:

  * case sensitivity
  * whole-word search
  * regex support
* Go to Line (`Ctrl+G`)
* Zoom in/out/reset
* Word wrap toggle

---

## Run & Debug

* **F5 Run** — execute Python scripts through `QProcess`
* **F6 Start Debug** — subprocess-based pdb debugger
* Full stepping controls:

  * Continue
  * Step Over
  * Step Into
  * Step Out
* Automatic editor jump to current execution line
* Free-form pdb commands:

  * `p var`
  * `pp dict`
  * `b 42`
  * `w`
  * etc.
* Stop execution:

  * `Shift+F5`
  * `Shift+F6`

---

## Integrated Terminal

* Persistent embedded PowerShell terminal
* Command history
* Restart & clear support
* `Ctrl+C` kills and restarts shell
* `Ctrl+`` focuses terminal
* Automatically syncs working directory with active file

---

## Visual Effects

### Ruby Red Title Bar

Uses Windows DWM API for immersive red title bars on Windows 11.

### Animated Video Background

Custom-rendered background video using `QVideoSink` instead of `QVideoWidget` for proper compositing and UI interaction.

### Glow Text Rendering

Blurred glow layer behind editor text using `QGraphicsBlurEffect`.

### Scrolling Code Marquee

Python syntax-highlighted scrolling banner beneath the menu bar with cached glow rendering.

### Matrix Rain

Animated falling red characters inside idle panels.

### Global Mouse Trail

System-wide glowing mouse trail overlay:

* Works outside the application window
* Works while minimized
* Python-style characters
* White-hot glow fading into dark ruby red

---

# Requirements

* Windows 10/11
* Python 3.10+ installed in PATH (required for Run/Debug)

The editor itself can still run without Python installed, but executing and debugging scripts requires a system Python installation.

---

# Shortcut Cheat Sheet

| Action                 | Shortcut                 |
| ---------------------- | ------------------------ |
| New / Open / Save      | Ctrl+N / Ctrl+O / Ctrl+S |
| Save As                | Ctrl+Shift+S             |
| Close Tab              | Ctrl+W                   |
| Find / Replace / Go To | Ctrl+F / Ctrl+H / Ctrl+G |
| Toggle Comment         | Ctrl+/                   |
| Duplicate Line         | Ctrl+D                   |
| Delete Line            | Ctrl+Shift+K             |
| Move Line              | Alt+↑ / Alt+↓            |
| Zoom                   | Ctrl+= / Ctrl+- / Ctrl+0 |
| Run / Stop             | F5 / Shift+F5            |
| Debug / Stop           | F6 / Shift+F6            |
| Continue / Step        | F8 / F10 / F11           |
| Focus Terminal         | Ctrl+`                   |

---

# Limitations

* No autocomplete
* No LSP integration
* No built-in file explorer
* `input()` is non-interactive in Run mode
* Debugger uses raw pdb commands
* Mouse trail does not appear over exclusive fullscreen applications
* Windows 11 required for custom ruby title bar
* Bundled EXE still requires system Python for Run/Debug features

---

# Project Structure

```txt
Stella Code/
├── main.py
├── requirements.txt
├── icon.png
├── icon.ico
├── recording.gif
├── background.mp4
├── Stella Code.cmd
├── register_open_with.py
└── README.md
```

---

# License

This project is licensed under the PolyForm Noncommercial License 1.0.0.

You may use, modify, and distribute this software for non-commercial purposes only.

Commercial usage is prohibited without explicit permission.

---

# Philosophy

Stella Code is not trying to replace VS Code.

It is an experimental, immersive, visually expressive coding environment focused on atmosphere, aesthetics, and interaction.

Built for people who want coding to feel cinematic.

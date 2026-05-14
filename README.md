<p align="center">
  <img src="logo.png" width="180" alt="Stella Code Logo">
</p>
# Stella Code

A visually stylized Python code editor built with PySide6.

Stella Code focuses on immersive visuals, smooth editing experience, and cyber-ruby aesthetics rather than becoming a full heavyweight IDE.

> Single-file application: `main.py` (~2300 lines).
> Intentionally minimal — no autocomplete, no file explorer, no splash screen.

---

# Features

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

* Python 3.10+
* PySide6 ≥ 6.6
* Windows 11 recommended
* H.264 codec support

Install:

```powershell
pip install PySide6
```

---

# Running

```powershell
cd "Stella Code"
pip install -r requirements.txt
python main.py
```

Open files directly:

```powershell
python main.py script.py another.py
```

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

# Build EXE (PyInstaller)

```powershell
pip install pyinstaller

pyinstaller --onedir --windowed --icon=icon.ico --name "Stella Code" `
  --add-data "icon.png;." `
  --add-data "icon.ico;." `
  --add-data "background.mp4;." `
  --collect-all PySide6 `
  main.py
```

Output:

```txt
dist/Stella Code/Stella Code.exe
```

---

# Windows "Open With" Registration

```powershell
python register_open_with.py
```

Uninstall:

```powershell
python register_open_with.py --uninstall
```

Per-user only. No administrator privileges required.

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
├── background.mp4
├── Stella Code.cmd
├── register_open_with.py
└── README.md
```

---

# Philosophy

Stella Code is not trying to replace VS Code.

It is an experimental, immersive, visually expressive coding environment focused on atmosphere, aesthetics, and interaction.

Built for people who want coding to feel cinematic.

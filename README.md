# psLauncher

**A portable, multi-language script launcher and manager for Windows.**

psLauncher is a lightweight desktop application built with Python and Tkinter that lets you organize, run, and monitor scripts written in virtually any scripting language — all from a single, searchable interface. No installation required; ship it as a single `.exe` and run it from anywhere.

![psLauncher screenshot](screenshot.png)

---

## Features

### Script management
- Add scripts individually or scan an entire directory tree (recursive option included)
- Supports `.py`, `.ps1`, `.bat`, `.cmd`, `.vbs`, `.js`, `.rb`, `.pl`, `.sh`, `.bash`, `.r`, `.php`, `.lua`, `.tcl`, `.ts`, `.go`, `.swift`, `.groovy`, `.awk`, `.sed`, and more
- Real-time search and filtering across the script library
- Group scripts into custom categories with a dedicated filter bar
- Pin frequently used scripts to the top of the list
- Rename, duplicate, or remove entries without touching the source files
- Export and import your entire script list as JSON for backup or sharing between machines

### Execution
- Per-script run options: custom interpreter, arguments, working directory, output encoding
- Run as Administrator (Windows UAC elevation)
- Hidden-window execution mode for background tasks
- Configurable PowerShell execution policy per script (`Bypass`, `RemoteSigned`, `Unrestricted`, `AllSigned`, `Restricted`, `Undefined`)
- Launch timeout — automatically kill a process after N seconds
- Auto-restart on crash, configurable per script
- Run an entire group sequentially with a single click
- Stop and restart running processes directly from the UI
- Run Profiles — save multiple named configurations (arguments, working directory, options) per script and switch between them instantly

### Sandbox mode
A built-in scratchpad environment for running ad-hoc commands and code snippets without adding them to your permanent script library. The sandbox automatically detects available interpreters on the host system, including:

Python, Bash/Shell, Node.js, Lua, Ruby, Perl, PHP, R, Tcl, Go, Java, .NET Script, TypeScript (ts-node), CoffeeScript, Elixir, and Windows Script Host (mshta).

Run the `runners` command inside the sandbox to list every interpreter currently detected on your system.

### Windows Explorer integration
Register a **"Run in Sandbox"** entry in the right-click context menu for script files directly from Explorer — no need to open psLauncher first. Selecting it launches psLauncher with the file pre-loaded into the sandbox, with the interpreter automatically inferred from the file extension. Registration and removal scripts are included and require no administrator privileges (writes only to `HKEY_CURRENT_USER`).

### Monitoring & diagnostics
- Execution log with timestamps for every run
- Export the log to a file at any time
- Per-script run history and run-count statistics
- Statistics dashboard summarizing usage across your entire library
- Live code preview for any script directly in the side panel
- Script metadata extraction — author, description, and version are parsed automatically from common comment conventions (`# version:`, `@version`, `$Version = '...'`, `__version__ = '...'`)

### Interface
- Bilingual UI — Polish and English, switchable at runtime
- Light and dark themes
- Drag-and-drop file support (via `tkinterdnd2`) for quickly adding scripts
- Drag-and-drop manual reordering of list entries
- Optional desktop notifications (via `plyer`)
- Optional global hotkeys (via the `keyboard` library) to trigger actions without focusing the window
- Full keyboard shortcut set: `F5`/`Enter` to run, `Del` to remove, `Ctrl+F` to search, `Ctrl+O` to add a script
- Right-click context menu for quick actions: run, dry run, run in sandbox, edit options, preview, rename, duplicate, open in Explorer, open terminal here, copy path, export launcher

---

## Installation

### Option 1 — Download the executable
Grab the latest `psLauncher.exe` from the [Releases](../../releases) page and run it directly. No installation, no dependencies, no admin rights required.

### Option 2 — Build from source
Requirements: Python 3.10+ and [PyInstaller](https://pyinstaller.org/).

```bash
git clone https://github.com/polsoft-seb07uk/psLauncher.git
cd psLauncher
pip install pyinstaller tkinterdnd2 plyer keyboard
pyinstaller psLauncher.spec
```

The compiled binary will be available at `dist/psLauncher.exe`, built as a single-file executable with the application icon and full Windows version metadata, and with the sandbox module compiled directly into the binary.

Alternatively, run `build.bat` for an interactive build menu (One-DIR or One-FILE).

---

## Enabling "Run in Sandbox" in Explorer

1. Copy `register_sandbox_context_menu.bat` into the same folder as `psLauncher.exe`.
2. Run it once — no administrator rights needed.
3. Right-click any supported script file in Explorer and select **Run in Sandbox**.

To remove the integration later, run `unregister_sandbox_context_menu.bat` from the same folder.

---

## Usage

1. Launch `psLauncher.exe`.
2. Add scripts manually (`Add`) or scan a folder (`Scan`) to populate your library.
3. Select a script and press `F5` or click `▶ Run`, or right-click for additional actions.
4. Use the side panel to inspect metadata, preview source code, or export the execution log.
5. Organize larger libraries into groups via the **Groups** menu, and assign Run Profiles to scripts that need multiple configurations.

---

## Project structure

```
psLauncher/
├── psLauncher.py              # Main application (Tkinter GUI)
├── sandbox.py                 # Sandbox module (interpreter detection, ad-hoc execution)
├── psLauncher.spec             # PyInstaller build specification (one-file)
├── build.bat                  # Interactive build script (One-DIR / One-FILE)
├── version_info.txt           # Windows version resource (EN/PL string tables)
├── psl.ico                    # Application icon
├── register_sandbox_context_menu.bat    # Adds "Run in Sandbox" to Explorer
└── unregister_sandbox_context_menu.bat  # Removes the Explorer integration
```

---

## Requirements

- Windows (primary target platform)
- Python 3.10+ (only required when building from source — the compiled `.exe` is fully self-contained)

Optional runtime libraries (gracefully degraded if absent):
- `tkinterdnd2` — drag-and-drop support
- `plyer` — desktop notifications
- `keyboard` — global hotkeys

---

## License

© 2026 Sebastian Januchowski & polsoft.ITS™. All rights reserved.

---

## Author

**Sebastian Januchowski** — polsoft.ITS™ Group
GitHub: [polsoft-seb07uk](https://github.com/polsoft-seb07uk)
Contact: polsoft.its@fastservice.com

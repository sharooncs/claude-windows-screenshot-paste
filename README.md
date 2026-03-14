# claude-windows-screenshot-paste

> A Claude Code skill that enables `Ctrl+V` screenshot pasting in the terminal on Windows.

**Author:** [@sharooncs](https://github.com/sharooncs)

---

Windows Terminal cannot natively paste images from the clipboard. This skill installs an AutoHotkey v2 script that intercepts `Ctrl+V`, saves clipboard images as PNG files, and types the file path into the terminal — so Claude can read them directly.

## Install as Plugin

```bash
/plugin marketplace add sharooncs/claude-windows-screenshot-paste
```

Then install the skill:

```powershell
powershell -ExecutionPolicy Bypass -File "${CLAUDE_SKILL_DIR}\scripts\install.ps1"
```

## Manual Install

1. Copy `skills/windows-screenshot-paste/` into `~/.claude/skills/`
2. Run the installer:

```powershell
powershell -ExecutionPolicy Bypass -File "$env:USERPROFILE\.claude\skills\windows-screenshot-paste\scripts\install.ps1"
```

## Usage

1. Press `Win+Shift+S` and snip any region of your screen
2. Click back into your terminal
3. Press `Ctrl+V`

The file path is typed automatically:
```
C:\Users\you\Pictures\Claude_Screenshots\Screenshot_20260314_163045.png
```

Claude reads the image from that path.

## Requirements

- Windows 10 or 11
- AutoHotkey v2 (installed automatically by the script)
- Windows Terminal, PowerShell, or CMD

## How It Works

- Only activates inside Windows Terminal, PowerShell, and CMD
- Detects bitmap on clipboard via Win32 `IsClipboardFormatAvailable` (CF_BITMAP=2, CF_DIB=8)
- Saves image via PowerShell's `System.Windows.Forms.Clipboard.GetImage()`
- Types the file path into the terminal with AutoHotkey `SendInput`

## Files

```
skills/
  windows-screenshot-paste/
    SKILL.md                  ← Claude skill instructions
    scripts/
      ClaudeScreenshot.ahk    ← AutoHotkey v2 script
      install.ps1             ← one-command installer
```

## License

MIT

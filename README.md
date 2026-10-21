# ARA Bridge

**[ARA Bridge](https://kirurg999.github.io/ARABridge/)** is a VST3/ARA plugin that sends audio from your DAW to an external audio editor and brings it back — seamlessly, with no real-time playback or bouncing required.

It was built to work around a Studio Pro bug that breaks iZotope's RX Connect, and it now works with many editors and with both Studio Pro (formerly PreSonus Studio One) and Cubase. Free, for Windows.

## Features

- **Round-trip editing** — send an audio event to your editor, save, and the edited audio plays back in the DAW immediately
- **iZotope RX Connect** — hosts RX 10 / 11 / 12 Connect directly, so the native *Send Back* workflow works in Studio Pro
- **Waveform preview** — blue for the original, green once the edited audio is back; stereo shown as separate L/R
- **Level meters and playback cursor**, with adjustable cursor delay to match DAW latency
- **Per-region editing** — sliced events are processed independently; *Revert changes* affects only the current region
- **Sample rate handling** — sources at a different rate from the project are resampled automatically
- **Saved with the project** — edits survive closing and reopening the song/project

## Supported DAWs

- **Fender Studio Pro** (tested with version 8)
- **Steinberg Cubase Pro** (tested with version 15)

## Supported Editors

Auto-detected from the Windows Registry:

- iZotope RX
- Steinberg SpectraLayers
- Steinberg WaveLab
- Adobe Audition
- MAGIX Sound Forge Pro
- Audacity
- ocenaudio
- Any other editor via the Browse (**...**) button or `scan.ini`

## Installation

1. Download the latest `ARABridge_x.x.x_Setup.exe` from [Releases](https://github.com/kirurg999/ARABridge/releases)
2. Close your DAW
3. Run the installer (requires admin rights — installs to `C:\Program Files\Common Files\VST3\`)
   > **Note:** Windows SmartScreen may show a warning. Click **"More info"** → **"Run anyway"**. This is normal for unsigned software.
4. Start your DAW

**Upgrading:** uninstalling the previous version first (Windows **Settings → Apps → ARA Bridge VST3**) is recommended. Your `scan.ini` and settings are kept.

## Usage

### Fender Studio Pro
1. Select an audio event
2. Open **ARA Bridge** from the ARA plugin section
3. Pick your editor from the dropdown
4. Click **"Send to Editor"**
5. Edit the audio, then **Save** (Ctrl+S)
6. Play — the audio is updated
7. Click **Render** to commit changes to the waveform

### Steinberg Cubase Pro
1. Select an audio event
2. Add **ARA Bridge** via Audio > Extensions
3. Pick your editor from the dropdown
4. Click **"Send to Editor"**
5. Edit the audio, then **Save** (Ctrl+S)
6. Play — the audio is updated
7. Use **Make Extension Permanent** or **Bounce Selection** to commit changes

### iZotope RX Connect
1. Pick **RX 1x Connect** from the dropdown and click **"Send to Editor"**
2. In the RX Connect window, click **Send** — the audio opens in RX Audio Editor
3. Edit in RX, then click **Send Back**
4. In ARA Bridge, click **Apply** when it shows *"Send Back received"*

You can save in RX and Send Back as many times as you like; each Send Back needs a new Apply.

### Plugin controls

| Control | What it does |
|---|---|
| **Revert changes** | Discards the edited audio for the current region and goes back to the original (asks first) |
| **Cursor delay** | Shifts the waveform cursor (0–2000 ms) so it lines up with what you hear when the DAW has heavy latency |
| **Temporary data...** | Chooses where exchange files are stored for this project |
| **Enable logging** | Writes diagnostic logs to `%APPDATA%\ARABridge\logs\` — attach these to bug reports |

Settings such as the selected editor and cursor delay are stored separately for each DAW.

## Requirements

- **Windows 11** (x64)
- **Fender Studio Pro** or **Steinberg Cubase Pro**
- An external audio editor

## Customizing the Editor List

Edit `%APPDATA%\ARABridge\scan.ini` to add or remove editors:

```ini
; Format: DisplayName | MinVersion | MaxVersion | ExeSubPath
; DisplayName is matched against installed programs; %d is the version number
RX %d | 9 | 15 | win64\iZotope RX %d Audio Editor.exe
SpectraLayers %d | 10 | 15 | Win-x86_64\SpectraLayers.exe
Audacity | 0 | 0 | Audacity.exe
```

Use `0 | 0` for editors without a version number in their name. RX Connect is detected separately and doesn't need an entry.

## Troubleshooting

**Plugin doesn't appear in Studio Pro's ARA list:**
- Ensure the VST3 is in `C:\Program Files\Common Files\VST3\ARA Bridge.vst3\`
- In Studio Pro, go to Options > Locations > VST Plug-Ins and click "Reset Blacklist"
- Restart Studio Pro

**Plugin doesn't appear in Cubase's Extensions:**
- Ensure the VST3 is in `C:\Program Files\Common Files\VST3\ARA Bridge.vst3\`
- Rescan plugins in Cubase's plug-in manager
- Restart Cubase

**No editors appear in the dropdown:**
- Check that `%APPDATA%\ARABridge\scan.ini` exists (the installer creates it)
- Verify your editors are installed and appear in Windows Add/Remove Programs
- Try the Browse (**...**) button to manually select an editor .exe

**RX Connect isn't in the dropdown:**
- The Connect VST3 must be in `C:\Program Files\Common Files\VST3\` or its `iZotope` subfolder (the RX installer puts it there)

**"Send Back unchanged - no edits detected":**
- RX sent back the same audio it received. Make an edit in RX before clicking Send Back.

**Waveform doesn't update after editing:**
- Studio Pro: click **Render** to refresh the visual — audio playback updates immediately
- Cubase: use **Make Extension Permanent** or **Bounce Selection** to commit changes
- This is a DAW limitation affecting all ARA plugins

**The info label is red with a "!":**
- The audio file's sample rate differs from the project's. Playback is resampled and correct; the warning is informational.

**Still stuck?** [Open an issue](https://github.com/kirurg999/ARABridge/issues/new/choose) with your DAW, editor and ARA Bridge versions, and a log file if you can.

## FAQ

**iZotope RX Connect doesn't work in Studio Pro / Studio One. What can I do?**
Install ARA Bridge, add it to the audio event as an ARA plugin, and pick **RX 10, 11 or 12 Connect** from its dropdown. ARA Bridge hosts RX Connect itself, so Send and Send Back work as they should. Click **Apply** when the audio comes back from RX.

**How do I send audio from Studio Pro or Cubase to iZotope RX Audio Editor and back?**
Pick your RX Audio Editor version in ARA Bridge and click **Send to Editor**. RX opens with the audio; edit it and press Ctrl+S. The edited audio plays back in the DAW straight away. See [Usage](#usage).

**Can I use SpectraLayers, WaveLab, Audition, Sound Forge or Audacity as an external editor?**
Yes. Installed editors are detected automatically. Any other editor can be added with the Browse (**...**) button or in [`scan.ini`](#customizing-the-editor-list).

**Does it work with PreSonus Studio One?**
Fender Studio Pro is the new name for Studio One. ARA Bridge is tested with Studio Pro 8. Earlier Studio One versions with ARA support may work but are untested.

**Does it change my original audio files?**
ARA Bridge never overwrites your source files. Edits are kept in separate files and played back in place of the original, and **Revert changes** goes back to the original. Committing an edit (Render in Studio Pro, Make Extension Permanent or Bounce Selection in Cubase) is done by the DAW itself.

**Is it free? Is there a Mac version?**
It's free. Windows 11 x64 only.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) or the [Releases](https://github.com/kirurg999/ARABridge/releases) page.

## About

Developed by Gunnar Ottenson.

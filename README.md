# ARA Bridge

**ARA Bridge** is a VST3/ARA plugin that sends audio from your DAW to an external audio editor and brings it back — seamlessly, with no real-time playback required.

It was built to work around a Studio Pro bug that breaks iZotope's RX Connect, but it works with multiple editors and DAWs.

## Supported DAWs

- **Fender Studio Pro** (tested with version 8)
- **Steinberg Cubase Pro** (tested with version 15)

## Supported Editors

Auto-detected from Windows Registry:

- iZotope RX 9–15
- Steinberg SpectraLayers 10–15
- Steinberg WaveLab 11–15
- Adobe Audition
- MAGIX Sound Forge Pro
- Audacity
- Ocenaudio
- Custom editors via Browse button or `scan.ini`

## Installation

1. Download the latest `ARABridge_x.x.x_Setup.exe` from [Releases](https://github.com/kirurg999/ARABridge/releases)
2. Run the installer (requires admin rights — installs to `C:\Program Files\Common Files\VST3\`)
   > **Note:** Windows SmartScreen may show a warning. Click **"More info"** → **"Run anyway"**. This is normal for unsigned software.
3. Restart your DAW

## Usage

### Fender Studio Pro
1. Select an audio event
2. Open **ARA Bridge** from the ARA plugin section
3. Pick your editor from the dropdown
4. Click **"Send to Editor"** (or enable "Auto-send on open")
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

## Requirements

- **Windows 11** (x64)
- **Fender Studio Pro** or **Steinberg Cubase Pro**
- An external audio editor

## Customizing the Editor List

Edit `%APPDATA%\ARABridge\scan.ini` to add or remove editors:

```ini
; Format: DisplayName | MinVersion | MaxVersion | ExeSubPath
RX %d | 9 | 15 | win64\iZotope RX %d Audio Editor.exe
SpectraLayers %d | 10 | 15 | Win-x86_64\SpectraLayers.exe
```

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
- Try the Browse (...) button to manually select an editor .exe

**Waveform doesn't update after editing:**
- Studio Pro: click **Render** to refresh the visual — audio playback updates immediately
- Cubase: use **Make Extension Permanent** or **Bounce Selection** to commit changes
- This is a DAW limitation affecting all ARA plugins

## About

Developed by Gunnar Ottenson.

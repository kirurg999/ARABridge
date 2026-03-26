# ARA Bridge

**ARA Bridge** is a VST3/ARA plugin for **Fender Studio Pro** that sends audio to an external audio editor and brings it back — seamlessly, with no real-time playback required.

It was built to work around a Studio Pro bug that breaks iZotope's RX Connect, but it works with multiple editors.

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
3. Restart Fender Studio Pro

## Usage

1. Select an audio event in Studio Pro
2. Open **ARA Bridge** from the ARA plugin section
3. Pick your editor from the dropdown
4. Click **"Send to Editor"** (or enable "Auto-send on open")
5. Edit the audio in the external editor, then **Save** (Ctrl+S)
6. Play in Studio Pro — the audio is updated

## Requirements

- **Windows 11** (x64)
- **Fender Studio Pro** (tested with version 8)
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

**No editors appear in the dropdown:**
- Check that `%APPDATA%\ARABridge\scan.ini` exists (the installer creates it)
- Verify your editors are installed and appear in Windows Add/Remove Programs
- Try the Browse (...) button to manually select an editor .exe

**Waveform doesn't update after editing:**
- This is a Studio Pro limitation affecting all ARA plugins (including WaveLab and SpectraLayers ARA)
- Click Studio Pro's "Render" button to refresh the visual — audio playback updates immediately

## About

Developed by Gunnar Ottenson.

# Changelog

All releases are Windows x64 betas. Installers are on the [Releases](https://github.com/kirurg999/ARABridge/releases) page.

## 1.0.20-beta — 2026-05-22

### Fixed
- Edits made in iZotope RX Audio Editor and saved were sometimes never applied to Studio Pro playback unless you pressed play straight away. Studio Pro recreates the playback region after a content change; ARA Bridge now keeps the edited audio through that, and picks up new edits regardless of transport state.

## 1.0.19-beta — 2026-05-09

### Added
- iZotope RX 12 Connect support.
- Every installed RX Connect version (10, 11, 12) appears as its own entry in the editor dropdown.

### Fixed
- Send Back now waits on the session folder of the RX version you selected (it always used RX 11's), so round trips with RX 10 and RX 12 complete reliably.

## 1.0.18-beta — 2026-04-02

### Fixed
- Sample rate mismatch when writing repaired audio returned from RX Connect.

## 1.0.17-beta — 2026-03-31

### Fixed
- Cubase: Revert didn't restore the original audio.
- Cubase: all events showed the same waveform when switching between them.

## 1.0.16-beta — 2026-03-31

### Fixed
- RX Connect: RX Audio Editor could stop responding after two rapid Send Backs.
- Revert removed edits from every region sharing the same audio; it now affects only the current region.

## 1.0.15-beta — 2026-03-31

### Removed
- "Auto-send on open" option.

## 1.0.14-beta — 2026-03-31

### Added
- iZotope RX 11 Connect integration: Send / Send Back workflow inside the DAW.
- **Apply** button to confirm before RX Send Back audio replaces the event.

### Fixed
- Stale audio when a shorter edit replaced a longer one.
- RX Connect not capturing reliably on the second session.
- Garbled characters in status messages.
- Cubase playback not updating after Apply.
- RX Connect session left open after Revert.

## 1.0.13-beta — 2026-03-29

### Changed
- Settings (selected editor, logging, cursor delay) are stored separately per DAW.
- Changing a setting in one plugin instance updates all other instances in the same session.

### Fixed
- Cubase: cursor and level meters now work.

## 1.0.12-beta — 2026-03-29

### Added
- Stereo waveform: left and right channels drawn separately.
- Level meters with PPM-style ballistics.

### Fixed
- Cubase: playback cursor didn't move.

## 1.0.11-beta — 2026-03-29

### Fixed
- Resampling works for any source/project sample rate combination.
- Crackle at audio block boundaries when resampling.
- Possible crash when reverting during playback.

### Changed
- Tighter UI layout; Revert is disabled until the waveform has loaded.

## 1.0.10-beta — 2026-03-28

### Fixed
- Audio recorded at a different sample rate from the project (e.g. 48 kHz in a 44.1 kHz project) now plays at the correct speed, both original and edited.

### Added
- Info label turns red when the source and project sample rates differ.

## 1.0.9-beta — 2026-03-28

### Fixed
- Volume bump when adding ARA Bridge to a track during playback (now fades in).
- Audio gaps when loading edited audio during playback.
- Editors that touch the file on open no longer trigger a false "audio updated".
- Lower CPU use from UI polling.

## 1.0.8-beta — 2026-03-28

### Added
- Cursor delay slider (0–2000 ms) to line up the waveform cursor with what you hear.

## 1.0.7-beta — 2026-03-28

### Added
- Playback cursor on the waveform.
- Durations over a minute shown as minutes and seconds.

## 1.0.6-beta — 2026-03-27

### Added
- Edits are saved with the project and restored when it reopens.
- **Revert changes** button (per region, with confirmation).
- **Temporary data...** button to choose where exchange files are stored, per project.
- Old temporary files and logs are cleaned up after 7 days.

### Fixed
- Removing and re-adding ARA Bridge now starts fresh instead of reusing old edits.
- File conflicts when several events used ARA Bridge at once.

## 1.0.5-beta — 2026-03-27

### Added
- Waveform preview: blue for the original, green for edited audio.
- Every save in the editor is picked up, including undo/redo cycles.

## 1.0.4-beta — 2026-03-27

### Added
- Plugin icon; minimum window size.

## 1.0.3-beta — 2026-03-27

### Added
- Sliced events: each region is processed independently.

### Fixed
- Cubase loaded the wrong region's audio in some cases.

## 1.0.2-beta — 2026-03-27

### Added
- Steinberg Cubase Pro 15 support via ARA Extensions, including Make Extension Permanent and Bounce Selection.
- Optional logging to `%APPDATA%\ARABridge\logs\`.
- Clear error when the exchange file is locked by the editor.
- Warning when inserted as a normal insert instead of an ARA extension.

### Fixed
- Studio Pro was detected as "Unknown" host.

## 1.0.1-beta — 2026-03-26

### Added
- Editor detection from the Windows Registry, configurable through `scan.ini`.
- Installer with icon and Add/Remove Programs entry.

### Fixed
- Crash hardening throughout ARA handling and settings I/O.

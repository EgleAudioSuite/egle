<div align="center">

<img src="assets/logo.png" alt="Egle logo" width="120" />

# Egle: Music Library Manager, HiFi Player & Mass Tag Editor for Windows

**All-in-one music suite for Windows: batch tag editor, bit-perfect HiFi player, FLAC authenticity checker, cover-art manager and an AutoEQ to Rockbox converter, all in a single 15 MB native app.**

[![Download](https://img.shields.io/badge/⬇%20Download-Get%20the%20app-7C3AED?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/EgleAudioSuite/egle/releases/latest)
[![Latest Release](https://img.shields.io/github/v/release/EgleAudioSuite/egle?style=for-the-badge&label=Latest&color=0EA5E9)](https://github.com/EgleAudioSuite/egle/releases/latest)
[![Platform](https://img.shields.io/badge/Windows-10%20%7C%2011-0078D6?style=for-the-badge&logo=windows&logoColor=white)](#system-requirements)
[![Support on Patreon](https://img.shields.io/badge/Support-Patreon-FF424D?style=for-the-badge&logo=patreon&logoColor=white)](https://www.patreon.com/cw/egleMusic)

[**⬇️ Download**](#-download) · [**✨ Features**](#-features) · [**🎧 Supported formats**](#-supported-formats) · [**💜 Support on Patreon**](https://www.patreon.com/cw/egleMusic)

</div>

---

## What is Egle?

**Egle** is a fast, native Windows desktop app to organize, clean, tag and play your music library. It puts together six tools that usually need five different programs:

- a **mass tag editor** that can auto-fix MP3 and FLAC tags, remove the "explicit" tag for you, tidy up genres and artist separators, renumber tracks and clear junk metadata across thousands of files at once;
- a **bit-perfect HiFi music player** with ReplayGain, gapless album playback and automatic sample-rate switching;
- a **music library manager** with albums, artists, genres, playlists, favorites, listening history, a duplicate finder and a 3D cover-flow view;
- a **FLAC authenticity checker** (real-time spectrogram) to spot fake or transcoded FLACs;
- a **cover-art / album-art batch manager** to embed, resize and clean artwork across formats;
- an **AutoEQ to Rockbox EQ converter** for your DAP.

It's built with Rust and Tauri, so it's a single light `.exe` (around 15 MB). No Electron bloat, no background services, no telemetry.

> 📥 You can download Egle directly. Grab the latest Windows build from the [**Releases**](https://github.com/EgleAudioSuite/egle/releases/latest) tab. If you want to support the project, there's also [Patreon](https://www.patreon.com/cw/egleMusic).

---

## 📸 Screenshots

<div align="center">

| Music Library | Now Playing |
|:---:|:---:|
| ![Music library manager for Windows](assets/screenshot-library.jpg) | ![HiFi bit-perfect now playing view with lyrics](assets/screenshot-nowplaying.jpg) |

| Picture Flow (3D cover flow) | Massive Tag Editor: easy tool to organize your library |
|:---:|:---:|
| ![3D cover flow view](assets/screenshot-pictureflow.jpg) | ![Mass tag editor to organize your music library](assets/screenshot-masstag.jpg) |

| DAP Manager (iPod / Rockbox / MP3 player sync) | AutoEQ to Rockbox EQ Converter |
|:---:|:---:|
| ![DAP manager syncing FLAC albums to an iPod or MP3 player](assets/screenshot-dap.jpg) | ![AutoEQ to Rockbox parametric EQ converter with response graph](assets/screenshot-eq.jpg) |

</div>

---

## ✨ Features

### 🧹 Massive Tag Editor: clean up your whole library

This is the tool most people open Egle for. You build a list of operations and run it on a folder or a set of files. You get a live diff preview before anything is written to disk, plus an in-memory Undo:

- Auto-fix MP3 / FLAC / M4A tags in bulk: clean whitespace, hidden BOM and zero-width characters, fix capitalization (Title / UPPER / lower / Sentence case).
- Remove the "explicit" tag automatically, and drop any non-standard junk tags (MusicBrainz, iTunes, foobar2000 leftovers). The recommended ones are pre-selected for you.
- Find and replace with plain text or regex across title, artist, album, genre and more.
- Normalize genres and values: merge spelling variants (like `Hip-Hop` vs `Hip Hop`) into one value, with auto-detection of the variants and manual targeting when you want it (for example map `Rap` to `Hip-Hop`).
- Normalize artist separators, dedupe featured artists, renumber tracks per disc, sync ARTIST and ALBUMARTIST.
- Apply cover art to many files at once, with Lanczos resize and JPEG quality control.
- Optional `.bak` backups for cross-session recovery.

### 🔊 Bit-Perfect HiFi Player

Lossless (FLAC / ALAC / WAV / AIFF) and lossy (MP3 / AAC / Vorbis / Opus) playback, powered by Symphonia and CPAL. Automatic per-track sample-rate switching, gapless album playback, ReplayGain (off / track / album), Windows media-key and SMTC integration, and a real Bit-Perfect badge that only lights up when there's no resampling in the chain.

### 🎼 Music Library Manager

An indexed database of your whole collection: albums, artists, tracks, genres, playlists, favorites, listening history and statistics. Flexible folder-layout scanning (Auto, Artist-Album, or a custom token template), instant search (`Ctrl+K`), and a 3D Picture Flow cover view with an optional spinning-vinyl skin.

There is also a built-in **duplicate finder**: it spots songs that appear more than once in your library (same artist and title, similar length), even when the copies are in different formats or quality, like the same track ripped to both FLAC and MP3. It marks the best copy of each group and lets you send the worse ones to the Recycle Bin in a couple of clicks, so cleaning up gigabytes of doubled music takes minutes, and nothing is ever deleted for good.

### 🏷️ Universal Tag Editor

Edit tags and lyrics (including synced LRC) on any supported format through one API. Vorbis Comments, ID3v2 and MP4 atoms are all handled the same way.

### 📃 Playlists with custom covers

Create and manage playlists, import and export them as M3U / M3U8 / PLS, set a custom cover image, and get an automatic 2x2 cover mosaic when you don't.

### 📈 FLAC Authenticity Checker

A real-time spectrogram (FFT) to spot fake or up-transcoded FLAC files at a glance.

### 🎚️ AutoEQ to Rockbox EQ Converter

Turn AutoEQ headphone profiles into native Rockbox `.cfg` parametric-EQ files, with biquad fitting (L-BFGS-B) and a live response graph. Batch import with sub-folder organization.

### 💿 Cover-Art / DAP Manager

Scan albums and embed, resize, extract or clean cover art across FLAC, MP3, M4A, OGG, WAV and AIFF. Handy when you're getting a Rockbox DAP ready.

### Plus

Portable mode · 7 languages (EN / IT / FR / ES / DE / PT / JA) · custom color-palette editor · full backup and restore to a single `.zip` · glass UI · guided onboarding tour.

---

## How Egle compares

A lot of people land on Egle coming from another music app, so here is where it fits. The whole point of Egle is simple: those tools each do one piece of the job, while Egle does all of it inside one app, with a clean modern look, and for free.

- **From Mp3tag or TagScanner:** the same batch tag editing you already know, plus a live preview of every change, an undo history and ready-made cleanup recipes. Egle does not stop at tags though. It also plays your music, manages your cover art and syncs your library to a DAP, all in the same window.
- **From MusicBee or MediaMonkey:** Egle is far lighter (one 15 MB app, installing is optional) and nicer to look at, and it still covers the full job: library, tagging, bit-perfect playback and DAP sync, without the clutter.
- **From foobar2000:** the bit-perfect playback you expect, but with a real bulk tag editor, a cover-art manager and a FLAC authenticity checker already built in, wrapped in a modern interface and with no extra components to track down.

One app instead of five, easy on the eyes, and free to download and use. Windows only for now.

---

## 🎧 Supported formats

| Format | Tags | Lossless |
|--------|:----:|:--------:|
| FLAC | ✅ | ✅ |
| MP3 | ✅ | ❌ |
| M4A / MP4 (AAC / ALAC) | ✅ | ALAC ✅ |
| AAC | ✅ | ❌ |
| OGG Vorbis | ✅ | ❌ |
| Opus | ✅ | ❌ |
| WAV | ✅ | ✅ |
| AIFF | ✅ | ✅ |

---

## ⬇️ Download

You can download Egle directly, no account needed.

- **📦 [Download from GitHub Releases](https://github.com/EgleAudioSuite/egle/releases/latest)**: the latest Windows build as a zip (`Egle_vX.Y.Z.zip`). Start here.
- **💜 [Egle on Patreon](https://www.patreon.com/cw/egleMusic)**: the same app, and the place to support development. Becoming a supporter unlocks higher limits and a few extra features (bigger libraries, more profiles, color palettes, picture-flow, backup).

### Installer or portable, your choice

The zip is not just a loose `.exe`. Inside you get both ways to run Egle, so pick the one you prefer:

- **Installer**: run the setup and Egle installs like a normal Windows app, with a Start menu shortcut and an uninstaller.
- **Portable**: just unzip and launch the `.exe`. Nothing gets installed and nothing is written to the system. It keeps its settings in a file right next to the executable, so it works great from a USB stick.

> Egle is closed-source freeware. This repository only holds the documentation and the release builds; the source code stays private. See [LICENSE](LICENSE).

---

## 🖥️ System requirements

- Windows 10 or 11 (64-bit)
- WebView2 runtime (already on Windows 11; the setup installs it on Windows 10)
- about 50 MB of free disk space

No .NET, no Java, no Python, no background services.

---

## 💜 Support

Egle is made by one person and it runs on Patreon support. If it saves you time with your music, becoming a [supporter](https://www.patreon.com/cw/egleMusic) helps a lot: it funds new features and keeps the app free for everyone.

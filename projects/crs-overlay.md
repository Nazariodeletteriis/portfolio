# CRS Overlay — Spotify controls, on top of a game

A Windows desktop overlay that shows and controls Spotify playback with global
shortcuts, sitting above a borderless fullscreen game. Personal project, written in
Rust.

## What it does

Changing a track while playing means leaving the game. This puts a small always-on-top
panel over it — current track, controls, keyboard shortcuts — and ducks the game audio
while Spotify is playing.

## Stack

Rust · Tauri 2 · React + TypeScript · Win32 API · Windows Core Audio · Spotify Web API

## Engineering highlights

**OAuth with PKCE, no client secret in the binary.** A secret shipped inside a desktop
app isn't a secret. The flow uses a generated verifier and challenge, catches the
callback on a local listener, and stores the refresh token in the Windows Credential
Manager — never in a config file, never in a log.

**The window is managed directly through Win32**: layered, always on top, never taking
focus, with click-through that can be toggled and three display modes.

**Audio ducking through Core Audio**, lowering the game's own mixer session while music
plays and restoring it on exit — with the API's limitation documented where it bites.

**A watch mode that costs nothing when idle.** Started with a flag, the app creates no
window at all: just a tray icon and a poll. The window appears when the game does, and
when the game closes the WebView gives its memory back.

**Compliance written before the code.** The project documents what it will not do —
no process memory reads, no graphics hooks, no low-level keyboard hooks, no synthetic
input, nothing hidden from screen capture — because that's the line between an overlay
and something an anti-cheat has every right to ban. Each module states which rule it
follows.

## Status

Working prototype, v0.1.0. Personal project, built over a weekend.

## Source code

Private for now.

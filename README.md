# 🏎️ Litomyšl Street Racing

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Play in browser](https://img.shields.io/badge/play-in%20browser-brightgreen.svg)](https://tjhavranek.github.io/race/)
[![Built with Pygbag](https://img.shields.io/badge/built%20with-Pygbag-blue.svg)](https://github.com/pygame-web/pygbag)
[![Made with Claude Code](https://img.shields.io/badge/made%20with-Claude%20Code-8A4FFF.svg)](https://docs.anthropic.com/en/docs/claude-code)

A two-player browser racing game set in Litomyšl, Czech Republic. Built by **Dan, Fila, and Lucinka** (ages 8–12) using [Claude Code](https://docs.anthropic.com/en/docs/claude-code) in about two hours — and then many more hours testing and improving it. Originally a gift for their cousins Kryštof and Kačka.

## ▶ [Play now in your browser](https://tjhavranek.github.io/race/)

No install needed. Works on desktop and on mobile (tap the fullscreen button when prompted).

![A top-down view of Litomyšl rendered in 1980s-style pixel art: nine landmark buildings labeled in Czech (Zámek Litomyšl, Smetanovo náměstí, Gymnázium A. Jiráska, ZŠ Zámecká, Smetanův dům, Muzeum, Kostel povýšení sv. Kříže, Piaristický klášter, Domov), a winding road network with 10 glowing checkpoint rings and scattered red bombs, the river Loučná running through, a blue Player 1 car near START and an orange Player 2 car near FINISH with an active "P2 IMMORTAL: 0.5s" cow power-up. A cow with the Litomyšl lily emblem stands near the museum; Smetana-portrait zombies are scattered across the streets.](docs/screenshot.png)

## The story

Our kids were sick and bored at home in February, so we introduced them to Claude Code. They did almost everything themselves — designing the track, setting the rules, picking the features. We only helped with publishing it on GitHub.

The graphics are charmingly 1980s. But it runs smoothly and it's fun.

## Controls

### Desktop (two players, one keyboard)

| Action        | Player 1 (blue)   | Player 2 (orange)                  |
|---------------|-------------------|------------------------------------|
| Accelerate    | `W`               | `↑`                                |
| Brake/Reverse | `S`               | `↓`                                |
| Steer left    | `A`               | `←`                                |
| Steer right   | `D`               | `→`                                |
| Fire          | `E` (after 5 s)   | `Enter` / `Right Ctrl` (after 5 s) |
| Start/Restart | `Space`           | `Space`                            |
| Menu/Exit     | `Esc`             | `Esc`                              |

### Mobile (one human + bot)

On touch devices, Player 2 becomes a bot. Touch the screen to steer, double-tap to fire.

## How to play

1. Wait for the **3-2-1 countdown** and race from **START** to **FINISH** through the streets of Litomyšl.
2. Pass all **10 checkpoints in order** — they're colored to show whose they are (blue = Player 1, orange = Player 2, purple = both).
3. You start with **2 lives** — look for the hearts above your car. Red bombs, opponent bullets, Smetana zombies, and crashes each cost you one life.
4. Watch out for **Smetana zombies** (they look like Bedřich Smetana's portrait, on legs) — they roam the streets and will chase you if you come within range.
5. Chase the **Litomyšl cows** — look for the white lily on a red shield (the town's coat of arms). Touching a cow gives you **5 seconds of immortality** and **permanently upgrades your weapon to rockets**, which one-shot anything and damage everything in an 80-pixel blast radius. Catch: a cow pickup briefly slows you for 2 seconds — that's the cost of the upgrade.
6. After the 5-second safe start, you can fire — `E` for Player 1, `Enter` or `Right Ctrl` for Player 2. Rockets (after a cow) replace bullets and can destroy bombs, zombies, and even buildings.
7. First across the finish line wins. If you finish in the global top 10, the game asks for your name.

## Features

- **9 destructible Litomyšl landmarks** — Zámek (Castle, UNESCO), Smetanovo náměstí, Gymnázium A. Jiráska, ZŠ Zámecká, Smetanův dům, Muzeum, Kostel povýšení sv. Kříže, Piaristický klášter, and Domov. They take damage in stages (scorch → cracks → fire → rubble). Yes, you can level the town.
- **Bullets vs rockets** — bullets cost the opponent one life; rockets (after a cow) are area-of-effect and one-shot anything.
- **Global top-10 leaderboard** shared in real time across all players worldwide.
- **All audio synthesized in pure Python** — engine, fire, explosions, dings, finish fanfare, and a looping 140 BPM track with melody, bass, and drums. No sample files in the bundle.
- Terrain (mountains, hills, the river Loučná) drawn beneath the track; fullscreen + mobile-landscape friendly.

## What's in this repo

| File | What it is |
|---|---|
| `index.html` | The Pygbag-generated runtime that loads the game in the browser. Hand-customized for mobile fullscreen. |
| `favicon.png` | Tab icon. |
| `litomysl-racing-game.apk` | The game itself. Despite the extension, it is a ZIP — Pygbag's bundling convention. Inside: `racing_game.py` (~4500 lines), `main.py`, the `smetana.png` portrait sprite, and the build scripts. |
| `docs/screenshot.png` | The screenshot above. |
| `.github/workflows/verify.yml` | CI guardrail — verifies the loader and icon haven't been accidentally modified, and (on manual dispatch) verifies the current APK fingerprint. |

To peek inside the bundle:

```bash
unzip litomysl-racing-game.apk -d unpacked
ls unpacked/assets/
```

## Building from source

The Python source lives inside `litomysl-racing-game.apk`. To rebuild the web bundle yourself after editing, see [CONTRIBUTING.md](CONTRIBUTING.md). A native desktop build is also possible with PyInstaller — see the `build_windows.bat` script inside the bundle.

## Notes

- **Audio needs a user gesture.** Modern browsers won't start music or sound effects until you click or press a key on the page (Web Audio policy). The very first menu interaction unlocks audio.
- **The leaderboard is a shared public store.** Times are persisted to a free public JSON endpoint (npoint.io). It's lightweight and there's no auth — which means a clever visitor could in principle clear or spam it. So far that has not happened.
- **Mobile fullscreen + landscape** are requested by the page; depending on the browser/OS, you may need to confirm a "fullscreen?" prompt before orientation locks.

## About Litomyšl

[Litomyšl](https://en.wikipedia.org/wiki/Litomy%C5%A1l) is a small historical town in eastern Bohemia, Czech Republic. Its Renaissance castle is a UNESCO World Heritage Site, the composer Bedřich Smetana was born there, and Smetanovo náměstí is one of the prettiest squares in the country.

## Takeaway

If kids can build a working game in two hours, you might be surprised what you can do.

## License

[MIT](LICENSE) — built by Dan, Fíla a Lucinka. Have fun.

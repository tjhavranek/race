# Contributing

Thanks for stopping by! This started as a weekend project — three kids (ages 8–12) building a racing game with [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — and it lives on as their playground. Contributions are welcome, but the project optimizes for *being a fun thing to tinker with*, not for production polish.

## How the project is built

The game is written in Python with [Pygame](https://www.pygame.org/) and compiled to WebAssembly by [Pygbag](https://github.com/pygame-web/pygbag). The deployed artifact is `litomysl-racing-game.apk` — despite the extension, it is a ZIP of the Python source plus assets (Pygbag's bundling convention).

The actual source files live inside that bundle. To inspect them:

```bash
unzip litomysl-racing-game.apk -d unpacked
ls unpacked/assets/
```

You will find `racing_game.py` (the game), `main.py` (the Pygbag entry point), `smetana.png` (a sprite of Bedřich Smetana, born in Litomyšl), and the Windows/web build scripts.

## How to propose a change

1. Fork the repo and make your change in a branch.
2. If you changed Python code, rebuild the web bundle:
   ```bash
   unzip litomysl-racing-game.apk -d work
   cd work/assets
   # apply your edits to racing_game.py, then:
   pip install pygame-ce pygbag
   bash build_web.sh        # or: build_web.bat on Windows
   ```
   Copy *only* the resulting `.apk` from `build/web/` into the repo root and rename it back to `litomysl-racing-game.apk`. Do not copy the generated `index.html` — the repo's `index.html` is hand-customized (mobile fullscreen, landscape hint) and replacing it would lose those tweaks and break the hash guardrail.
3. Open a pull request describing what you changed and how to test it.

## Files you should not edit for documentation-only changes

- `index.html`
- `favicon.png`
- `litomysl-racing-game.apk`

These three define the deployed game. The CI workflow verifies the first two on every push.

## What you don't need to worry about

- No lint config, no formatter — match what's already there.
- No test suite. Manual play-through is the test.
- The history has many "Delete .apk / Add files via upload" pairs. That's GitHub's web UI for replacing a file. Leave the history alone.

## Code of conduct

Be kind. This is a kids' project; comments and reviews should be encouraging.

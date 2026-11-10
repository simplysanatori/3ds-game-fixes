# AGENTS.md

Technical detail kept out of the README: how the repo is laid out and how a fix is added. Each game's own `AGENTS.md` explains its fix.

## Layout

```
games/<game>-<region>/
  README.md                     short page for players
  AGENTS.md                     how the fix was found and how it works
  patch/<title id>/code.ips     IPS against the decompressed ExeFS .code
  cheats/<title id>.txt         Action Replay codes, Citra/Azahar file format
  images/                       before/after screenshots
docs/USER_GUIDE.md              install folders for every emulator, shared by all games
```

- Folder names are lowercase, with the region last: `stella-glow-usa`, `dragon-quest-xi-usa`.
- The `patch/<title id>/` folder mirrors the mods folder, so it can be copied in whole.
- Fixes live as folders on `main`, one per game. Use a branch only for a fix still in progress, then merge it.
- Add each new game to the **Games** list in `README.md`.

## Rules for a fix

- **Cheats:** use only standard Gateway/Action Replay opcodes, so they work in Azahar, Citra, Zakuro, Rosalina and CTRPF.
- **Guards:** guard every code-region write with a type-5 compare against the original word and close it with `D0000000 00000000`. End the file with `D2000000 00000000`. Then it writes once and does nothing on another version.
- **Patch and cheat:** ship the same change as `code.ips`. IPS offsets are relative to the decompressed `.code`: address minus `0x00100000`.
- **Version:** name the game version the fix targets: cartridge `rev<remaster version>` or `update <major>.<minor>`.
- **Testing:** test in at least one emulator with before/after screenshots of the same scene. List what wasn't tested in the game's README.
- **Two fixes for one game:** a game gets one `code.ips`. Merge the records into one file rather than shipping two patches for the same game.

## Tools used

- [Zakuro](https://github.com/fearkov/zakuro) headless harness (`crates/zakuro-core/examples/boot.rs`): scripted input, save states, screen dumps and GPU trace logs.
- Capstone, for disassembling the decompressed `.code`.
- Azahar's Ctrl+P screenshots, for before/after images.

## How this was made

I started this project and used AI (Claude) to speed up development. I write, review and fix code by hand all the way through, keep the AI's work checked and reined in, and aim to keep the patches as lightweight as possible. I test them in Azahar and Zakuro on my own PC.

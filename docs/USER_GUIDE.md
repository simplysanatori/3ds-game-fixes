# User guide

## Which file to use

- `patch/0004000000173700/code.ips` is applied when the game starts. It needs no cheat menu. Use this one.
- `cheats/0004000000173700.txt` is an Action Replay code. Use it only where mods aren't available.

The patch and the cheat make the same change. Using both does no harm.

## Install locations

| Where | Put `code.ips` in |
|---|---|
| Azahar / Citra (Windows) | `%APPDATA%\Azahar\load\mods\0004000000173700\` (Citra: `%APPDATA%\Citra\load\mods\0004000000173700\`) |
| Azahar / Citra (any system) | Right-click the game, **Open Mods Location** |
| Zakuro | `%APPDATA%\zakuro\mods\0004000000173700\` (Windows), `~/.local/share/zakuro/mods/0004000000173700/` (Linux) |
| Real 3DS (Luma3DS) | `luma/titles/0004000000173700/` on the SD card |

Azahar and Citra also accept `exefs/code.ips` inside the mods folder.

## Real 3DS

1. Copy `code.ips` to `luma/titles/0004000000173700/` on the SD card.
2. Hold **Select** while powering on to open the Luma3DS config.
3. Turn on **Enable game patching**, then save.

To use the cheat instead, load it through the Rosalina menu (L + Down + Select) **Cheats** or through CTRPF.

## Zakuro

Zakuro runs recompiled game code. After adding `code.ips`, press **Recompile** next to the game once. Otherwise the patched part runs slower through the interpreter.

## Troubleshooting

- **Glow still there.** The patch only fits the USA release with title ID `0004000000173700`. On another version the cheat does nothing, and the patch may have no effect.
- **Cheat does nothing.** Some emulators keep running already-translated code after a cheat changes it. Use the patch file instead.
- **Scene looks darker at 1x.** The game's intended soft glow is removed too. That's expected.
- **The file isn't picked up.** It must be named exactly `code.ips`, in a folder named `0004000000173700`.

## Reporting a problem

Open an issue with:
- your emulator or 3DS and its version;
- your game region;
- whether you used the patch or the cheat;
- a screenshot of the scene.

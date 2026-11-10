# User guide

## Patch or cheat?

- **`code.ips`**: use this one. It doesn't require a cheat menu, and it's on every time you start the game.
- **Cheat**: use this if you can't use mods.

You can use both at once. It doesn't do anything extra.

## Where `code.ips` goes

| Where | Folder |
|---|---|
| Azahar / Citra | Right-click the game, **Open Mods Location** |
| Azahar (Windows) | `%APPDATA%\Azahar\load\mods\0004000000173700\` |
| Citra (Windows) | `%APPDATA%\Citra\load\mods\0004000000173700\` |
| Zakuro (Windows) | `%APPDATA%\zakuro\mods\0004000000173700\` |
| Zakuro (Linux) | `~/.local/share/zakuro/mods/0004000000173700/` |
| Real 3DS (Luma3DS) | `luma/titles/0004000000173700/` on the SD card |

The file has to be named `code.ips`. An `exefs` folder inside the mods folder works too.

## Zakuro

1. Click **Mods** next to Stella Glow in the library.
2. Copy `code.ips` into that folder.
3. Press **Recompile** next to the game.

Recompiling builds the patch into the game's recompiled code. If you skip it, the patch still works, but that part of the game runs slower.

To use the cheat instead, open the menu with **Esc**, go to **Cheats**, paste the code and turn it on. Zakuro switches the patched code back to its slower interpreter, so the patch file is the better pick here.

## Real 3DS

1. Copy `code.ips` to `luma/titles/0004000000173700/` on the SD card.
2. Hold **Select** while turning the 3DS on.
3. Turn on **Enable game patching** and save.

For the cheat, use the Rosalina menu (**L + Down + Select**, then **Cheats**) or CTRPF.

## Troubleshooting

- **Glow is still there.** You need the USA release, title ID `0004000000173700`.
- **The cheat does nothing.** Use the patch file instead.
- **The patch isn't picked up.** Check the file is named `code.ips` and the folder is `0004000000173700`.
- **The game looks a bit darker at 1x.** The game's own soft glow is gone too. That's expected.

## Reporting a problem

Open an issue with:

- your emulator or 3DS, and its version
- your game region
- patch or cheat
- a screenshot of the scene

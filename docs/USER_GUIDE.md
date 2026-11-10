# User guide

## Patch or cheat?

- **`code.ips`**: use this one. It doesn't require a cheat menu, and it's on every time you start the game.
- **Cheat**: use this if you can't use mods.

You can use both at once. It doesn't do anything extra.

## Where `code.ips` goes

Replace `<title ID>` with the ID from the game's folder.

| Where | Folder |
|---|---|
| Azahar / Citra | Right-click the game, **Open Mods Location** |
| Azahar (Windows) | `%APPDATA%\Azahar\load\mods\<title ID>\` |
| Citra (Windows) | `%APPDATA%\Citra\load\mods\<title ID>\` |
| Zakuro (Windows) | `%APPDATA%\zakuro\mods\<title ID>\` |
| Zakuro (Linux) | `~/.local/share/zakuro/mods/<title ID>/` |
| Real 3DS (Luma3DS) | `luma/titles/<title ID>/` on the SD card |

The file has to be named `code.ips`. An `exefs` folder inside the mods folder works too. A game can only have one `code.ips`, so two patches can't both be copied in.

## Cheats

The cheat files use the standard Action Replay format. Each code checks for the original game code before it writes, so on the wrong version it does nothing.

- **Azahar / Citra:** copy the `.txt` into `%APPDATA%\Azahar\cheats\`, then turn it on under **Emulation**, **Configure Current Game**, **Cheats**.
- **Zakuro:** press **Esc**, go to **Cheats**, paste the code and turn it on.
- **Real 3DS:** the Rosalina menu (**L + Down + Select**, then **Cheats**) or CTRPF.

## Zakuro

1. Click **Mods** next to the game in the library.
2. Copy `code.ips` into that folder.
3. Press **Recompile** next to the game.

Recompiling builds the patch into the game's recompiled code. If you skip it, the patch still works, but that part of the game runs slower. Cheats that change game code also run slower in Zakuro, so the patch file is the better pick there.

## Real 3DS

1. Copy `code.ips` to `luma/titles/<title ID>/` on the SD card.
2. Hold **Select** while turning the 3DS on.
3. Turn on **Enable game patching** and save.

## Troubleshooting

- **The fix doesn't work.** Check your game's region and title ID match the game's folder.
- **The cheat does nothing.** Use the patch file instead.
- **The patch isn't picked up.** Check the file is named `code.ips` and the folder is the title ID.
- **You have an update installed.** Each fix is made for the version its folder names.

## Reporting a problem

Open an issue with:

- the game and its region
- your emulator or 3DS, and its version
- patch or cheat
- a screenshot of the scene

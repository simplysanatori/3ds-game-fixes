# 3DS Game Fixes

Patches and cheats that fix graphics bugs and add tweaks to 3DS games. They work in Azahar, Citra, Zakuro and on a real 3DS with Luma3DS.

## Games

- [Stella Glow (USA)](games/stella-glow-usa/): removes the ghostly glow around characters at high resolution

## How it works

- Each game has its own folder under `games/`.
- Most fixes come as a patch file (`code.ips`) and as a cheat code.
- The patch changes the game's code when it starts. The cheat does the same change from the cheat menu.
- Each fix is made for one region and version of the game. It does nothing on a different version.

## Requirements

- Your own copy of the game, in the region the game's folder names
- Azahar, Citra or Zakuro, or a 3DS with Luma3DS

## Install

1. Open the game's folder and find its title ID, for example `0004000000173700`.
2. Copy `patch/<title ID>/code.ips` into your emulator's mods folder for that game:
   - Azahar / Citra: right-click the game and choose **Open Mods Location**
   - Zakuro: click **Mods** next to the game, then press **Recompile**
   - Real 3DS: `luma/titles/<title ID>/` on the SD card, with **Enable game patching** on in Luma3DS
3. Start the game.

The file has to be named `code.ips`. Use the cheat in `cheats/<title ID>.txt` only if you can't use mods.

## Uninstall

Delete `code.ips` from the mods folder, or turn off the cheat.

## Troubleshooting

- Fix doesn't work: check your game's region and title ID match the folder.
- The cheat does nothing: use the patch file instead.
- The patch isn't picked up: the file must be named `code.ips`.

## More

- [User guide](docs/USER_GUIDE.md): install folders for each emulator, cheats, real 3DS
- [AGENTS.md](AGENTS.md): how the repo is laid out and how fixes are made, for developers and AI agents
- Each game folder has an `AGENTS.md` with how its fix works

## Support

https://ko-fi.com/sana748653

## Credits

- [Zakuro](https://github.com/fearkov/zakuro): the 3DS emulator used to trace and test fixes

## Licence

MIT

## How this was made

I started this project and used AI (Claude) to speed up development. I write, review and fix code by hand all the way through, keep the AI's work checked and reined in, and aim to keep the patches as lightweight as possible. I test them in Azahar and Zakuro on my own PC.

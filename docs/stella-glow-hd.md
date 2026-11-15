# Stella Glow HD

An HD texture pack for Stella Glow: every texture upscaled 4x, with the UI text, logos and turn-order portraits redrawn by hand.

Version 0.9.0, by [simplysanatori](https://github.com/simplysanatori). Made on the USA version.

## What's in it

- Character sprites, portraits and battle portraits
- 3D characters, weapons and event CGs
- Menus, battle UI, dialogue boxes, title and chapter cards, staff roll
- About 14,700 textures, about 4.7 GB

Pair it with [No Bloom](../games/stella-glow-usa/). The ghost outlines around characters at high resolution don't come from a texture, so the pack alone can't remove them.

## How it was made

- Each texture was upscaled 4x with an AI upscaler, in overlapping tiles so no seams show.
- Transparency was upscaled on its own, to keep edges clean.
- UI text, logos and the turn-order portraits were redrawn by hand.
- The pack is PNG files with a `pack.json`, in the standard Azahar and Citra layout.
- In Azahar for Frame, **Optimize for Frame** makes an ASTC copy on the headset. It loads faster and uses a quarter of the GPU memory. Only the PNG pack is downloaded.

## Requirements

- Your own copy of Stella Glow (USA), title ID `0004000000173700`
- Azahar for Frame, Azahar or Citra
- About 5 GB free, and as much again for the optimized copy

## Install in Azahar for Frame

1. Start Stella Glow and open the in-game menu.
2. Go to **Mods**, then **Textures**, then **Download Packs**.
3. Press **Download** on **Stella Glow HD**.
4. Make sure its checkbox is ticked.
5. When **Optimize Stella Glow HD for Frame?** shows, press **Optimize**.

Leave **Preload** off. The pack is too large to preload, so it loads as you play.

## Install by hand

1. Download [Stella Glow HD.zip](https://drive.google.com/file/d/1XSi6l-QUmFrzYL4flQe6wZu1NGR859w_/view) and unzip it.
2. Open the texture folder for the game:
   - Azahar: right-click the game, **Open**, **Custom Texture Location** (Citra has the same in its right-click menu)
   - Azahar for Frame: `~/.local/share/AzaharFrame/user/load/textures/0004000000173700/`
3. Copy what's inside the `Stella Glow HD` folder there. `pack.json` goes directly in that folder.
4. Turn on **Use custom textures** in the graphics settings, if it's off.

## Uninstall

In Azahar for Frame, press **Delete** on the pack under **Download Packs**. Otherwise delete the files from the texture folder.

## Licence

Free for emulators; credit the author.

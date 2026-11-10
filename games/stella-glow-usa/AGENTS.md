# AGENTS.md

Technical detail moved out of the README: what the bug is, how the patch works and how it was verified.

## Target

- Stella Glow (USA), title ID `0004000000173700`, cartridge executable, remaster version 0 (`rev0` in Zakuro's terms).
- `.code` is BLZ-compressed in ExeFS and loads at `0x00100000`. All addresses below are virtual addresses in the decompressed code.
- No update was available to test against. The cheat's guards stop it writing on a different executable. The IPS has no guard.

## The bloom pass (measured)

The game builds its glow in one command list, every few frames:

1. Draws the scene into the main colour buffer (phys `0x18000000`, 256x512 RGBA8).
2. **Downsample:** draws one bilinear quad that samples the scene into a 64x64 target at phys `0x18400100`.
3. Draws an untextured quad with colour 0.3 over the same target, with blend `0x16160202`.
4. **Blur:** draws 8 quads that sample `0x18400100` into a second 64x64 target at `0x18404180`. Each quad is offset by ±1.25 texels, has vertex alpha 0.15 and blends additively.
5. **Composite:** draws a full-screen additive quad that samples `0x18404180` onto the main buffer, with vertex colour (1,1,1,1).

There are no downscaling display transfers or TextureCopy commands in the chain. The parameters (10.0, 0.3, 0.15) appear as `GLAREPARAM` rows in `romfs/param/battlegra_param.bin`.

## Why it breaks when upscaled

At 1x, each blur tap bilinearly mixes neighbouring texels of a coarse 64x64 image, so the 8 taps merge into a soft glow. Emulators scale render targets by N, so at Nx the 64x64 targets become 64N x 64N. The downsample keeps N times more detail, and the 1.25-texel taps land 1.25N host pixels apart. Each tap then shows as a sharp, separate copy of the character. This is why the effect grows with every resolution step. Texture packs replace textures, not render targets, so they cannot affect it.

## The patch

- Bloom function: `0x109134`–`0x1095C4`, called only from `0x105404` and `0x105670`, both in the same routine.
- The composite is drawn by `bl 0x214954` at `0x109598`. Its colour array at `sp+8..sp+0x14` is filled by four `vstr s22` stores, with `s22` = 1.0.
- The patch changes those four ARM instructions to store `s23` instead:

| Address | Original | Patched |
|---|---|---|
| `0x109558` | `ED8DBA02` `vstr s22,[sp,#8]` | `EDCDBA02` `vstr s23,[sp,#8]` |
| `0x109560` | `ED8DBA03` | `EDCDBA03` |
| `0x109564` | `ED8DBA04` | `EDCDBA04` |
| `0x109568` | `ED8DBA05` | `EDCDBA05` |

- `s23` is loaded once at `0x109280` (`vldr s23,[pc,#0x35c]`) from the literal at `0x1095E4`, which is 0.0. The only branch before that load is the early exit at `0x10914C`. `s23` is never written afterwards, and `s16`–`s31` are callee-saved, so it is 0.0 at every store.
- With the composite colour zeroed, the additive blend adds nothing. The rest of the pass still runs but has no visible effect.
- An earlier attempt zeroed the composite vertices in the linear heap. It failed: the game rewrites that buffer every frame, and the address moves.
- Possible cleaner switch, untested: the byte at `[0x2F6428]` gates the whole function through the early exit at `0x10914C`.

## Files

- `patch/0004000000173700/code.ips`: 4 IPS records at file offsets `0x9558`, `0x9560`, `0x9564` and `0x9568`, relative to the decompressed `.code`.
- `cheats/0004000000173700.txt`: Gateway/Action Replay format. Each write is guarded by a type-5 compare against the original word and closed with `D0000000`, and the file ends with `D2000000`. It writes only when the original code is present, so it writes once and does nothing on other versions.

## Verification

- **Zakuro headless harness**, 1x and 4x, on the battle map at frame 13000:
  - The 4x ghosts and the cursor stripes are gone.
  - The result is pixel-identical (RMSE 0) to the same build with the composite draw skipped.
  - Frames 2000, 9000 and 16000 render correctly.
- **Azahar 2125.0.1** at 6x, Vulkan, in the Mithra village scene loaded from a real save:
  - The cheat, loaded on a save state, removes the halos.
  - `code.ips` alone, on a fresh boot, removes the halos too.
- **Not yet tested:**
  - real hardware (Luma3DS / CTRPF);
  - Citra;
  - a battle in Azahar;
  - every cutscene type.

## Emulator-side fix (Zakuro)

A separate Zakuro change keeps the glow and renders it correctly when upscaled. It is behind `ZAKURO_BLOOM_FIX=1` and is not part of this repo. It keeps render targets of 64x64 or smaller at 1x, and box-averages a scaled buffer when a smaller-scale target samples it. Output at 1x is byte-identical with and without it.

## Zakuro and 3dsrecomp notes

- Zakuro loads `code.bin`, `code.ips` or `code.bps` from `mods/<title id>/` or `mods/<title id>/exefs/` (see `crates/zakuro-core/src/mods.rs`). 3dsrecomp builds from the patched code when the mod is present at **Recompile** time.
- Cheat writes to code go through `write32_privileged`. With a recompiled library loaded, Zakuro calls `library.check()` and runs the changed functions in the interpreter, which is slower.
- The cheat could ship as a built-in Zakuro enhancement. That means an entry in `crates/zakuro-core/src/enhancements.txt` under `= 0004000000173700 Stella Glow (USA)` with build `rev0`. It would need a PR upstream. Turning an enhancement off restores the overwritten words.
- 3dsrecomp also supports `RECOMP_OVERRIDE` C functions (`docs/overrides.md`). An override is not needed here, because the IPS is compiled in.

## How this was made

I started this project and used AI (Claude) to speed up development. I write, review and fix code by hand all the way through, keep the AI's work checked and reined in, and aim to keep the patch as lightweight as possible. I test it in Azahar and Zakuro on my own PC.

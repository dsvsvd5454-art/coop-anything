# God of War Ragnarök

| | |
|---|---|
| Engine | Santa Monica Studio proprietary (Kinetica lineage; Ragnarök adds SMS visual scripting per studio talks). PC port by Jetpack Interactive. |
| Versions tested | **None this session.** Public identity: Steam AppID `2322010`, PC release 2024-09-19, main exe named `GoWR.exe` in mod docs. Owner build id / SHA-256: unknown. |
| Projects | **No public co-op mod found.** Single-player tooling: [Eiton/GoWR-Script-Loader](https://github.com/Eiton/GoWR-Script-Loader) (MIT), [GoWR MIO](https://www.nexusmods.com/godofwarragnarok/mods/202), [iArtorias/smpack](https://github.com/iArtorias/smpack). Same-engine prior art: [God of War (2018) write-up](../god-of-war-2018/README.md). |
| QA level | `none` (triage/research only; no co-op client tested) |
| Last updated | 2026-11-10 |

## Where things stand

Nobody can play *God of War Ragnarök* story co-op via a public mod today. Retail PC/console builds are single-player. Triage verdict: **build from zero** (nothing usable to revive), reusing lessons and patterns from the in-repo GoW 2018 Kratos+Atreus prototype and Ragnarök's existing `winmm.dll` script loaders — after the owner supplies a hashed PC install for a test copy.

## Existing work

Searched 2026-11-10: this repo's directory / `games/` / PRs, upstream `cranebeaker/coop-anything` issues & PRs, GitHub repository search, Nexus Mods, ModDB, Steam/PCGamingWiki/PlayStation Blog, and the REAC 2024 Santa Monica Studio talk PDF. Raw notes: [NOTES.md](NOTES.md).

- **Co-op / multiplayer mods:** Not found on GitHub, Nexus, or ModDB (ModDB mods list empty for this game).
- **[Eiton/GoWR-Script-Loader](https://github.com/Eiton/GoWR-Script-Loader)** (MIT; releases through `1.2` on 2026-03-28): dumps scripts and loads replacements without repacking; installs as `winmm.dll` next to `GoWR.exe`.
- **[GoWR MIO](https://www.nexusmods.com/godofwarragnarok/mods/202):** Script dump/load for Lua and SMS visual scripts, plus SP QoL patches; compatible with Eiton's `mod\` layout.
- **Nexus SP mods** (examples): Revamped Combat (Lua under `mod/int9/gameart/scripts/characters/heroa00/`), companion swaps limited to Hrólf arena — not network co-op.
- **God of War (2018) in this repo:** Working asymmetric Atreus network prototype documented under [games/god-of-war-2018](../god-of-war-2018/README.md). That is a **different executable and WAD set**; addresses and APIs do not transfer without re-mapping on Ragnarök.

## How the game works (for co-op)

From public sources only (no local `GoWR.exe` this session):

- Content ships in **WADs**; characters are WADs (studio REAC 2024 talk).
- Ragnarök introduced **visual scripting** intended to replace much of the previous Lua scripting (same talk; GDC 2023 SMS presentation linked from it). PC mods still inject **Lua** for hero behaviour via Script-Loader / GoWR MIO.
- Retail build has **no multiplayer netcode** advertised. Whether `GoWR.exe` still embeds LuaSocket/`cmsgpack` like GoW 2018 is **unknown** until a test copy is analyzed.
- Saves: `%USERPROFILE%\Saved Games\God of War Ragnarök\` (PCGamingWiki).

Likely co-op design (guess, pending RE): asymmetric **Kratos host + companion client** (Atreus and/or Freya), host-authoritative world — same shape as the 2018 prototype, not verified on Ragnarök.

## What we changed

Triage contribution only: directory gap entry, this write-up, and NOTES. No game binary patches and no co-op package.

## QA

Not applicable yet (`qa: none`). Do not claim co-op works.

## How to play

N/A — no co-op build.

## Known issues

N/A for co-op. Research gaps listed in [NOTES.md](NOTES.md).

## Next steps

1. Owner: confirm store/version, provide install path for a **copied** test tree, SHA-256 of `GoWR.exe`, approve claim-issue posting (fork Issues currently disabled).
2. Phase 2 workspace: isolated copy, Script-Loader for dumps only (ask before downloading).
3. Phase 3: map companion VMs, confirm sockets/serialization, compare to GoW 2018 hooks.
4. Phase 4–5: design doc then build-from-zero sync (fake world / fuzzer before live clients).

## Sources

- https://store.steampowered.com/app/2322010/God_of_War_Ragnarok/
- https://blog.playstation.com/2024/05/30/god-of-war-ragnarok-is-coming-to-pc/
- https://www.pcgamingwiki.com/wiki/God_of_War_Ragnar%C3%B6k
- https://github.com/Eiton/GoWR-Script-Loader
- https://www.nexusmods.com/games/godofwarragnarok
- https://www.nexusmods.com/godofwarragnarok/mods/202
- https://www.nexusmods.com/site/mods/959
- https://www.moddb.com/games/god-of-war-ragnark/mods
- https://enginearchitecture.org/downloads/REAC_2024_SMS.pdf
- https://game8.co/games/God-of-War-Ragnarok/archives/396034
- ../god-of-war-2018/README.md

# God of War Ragnarök — Phase 0 triage notes

Date: 2026-11-10
Status: Phase 0 (Triage) + Phase 1 research from public sources only. No owner install, no game process, no downloads, no tools installed this session.

Slug: `god-of-war-ragnarok`

## 1. Which exact game?

### Observations (public sources)

- **Title:** God of War Ragnarök (also marketed as God of War Ragnarok).
- **Developers:** Santa Monica Studio; PC port with Jetpack Interactive (PlayStation Blog; Steam store).
- **Publishers:** PlayStation Publishing / PlayStation PC.
- **Console release:** 2022-11-09 (PS4/PS5) — widely reported; not re-verified against a primary Sony page this session beyond PlayStation Blog PC announcement context.
- **PC release:** 2024-09-19 ([PlayStation Blog](https://blog.playstation.com/2024/05/30/god-of-war-ragnarok-is-coming-to-pc/), [Steam](https://store.steampowered.com/app/2322010/God_of_War_Ragnarok/), [PCGamingWiki](https://www.pcgamingwiki.com/wiki/God_of_War_Ragnar%C3%B6k)).
- **Steam AppID:** `2322010` (Steam / SteamDB / PCGamingWiki).
- **Mode:** Single-player only on retail PC/console (Game8; PCGamingWiki taxonomy; ModDB game page). Valhalla DLC ships with PC and is also single-player.
- **Main executable name (mod docs):** `GoWR.exe` ([Eiton/GoWR-Script-Loader](https://github.com/Eiton/GoWR-Script-Loader), [GoWR MIO on Nexus](https://www.nexusmods.com/godofwarragnarok/mods/202)).
- **Saves (PCGamingWiki):** `%USERPROFILE%\Saved Games\God of War Ragnarök\` (and `settings.ini` under the game/profile layout described there).

### Unknowns (need owner / local install)

- Owner's store (Steam vs Epic).
- Exact build id / `GoWR.exe` file version / SHA-256.
- Whether `exec/boot-options.json` (or Ragnarök equivalent) is present and what `code-branch` / changelist it reports.
- Owner install path (for a **copied** test tree only — never touch the live install or saves).

## 2. Is it already done? (directory, issues/PRs, external)

### This repo

- **`DIRECTORY.md` / `data/directory.yaml`:** Entry exists for **God of War (2018)** only (`kind: gap` historically updated with a built prototype note; `checked: 2026-10-28`). **No directory entry for God of War Ragnarök** before this session.
- **`games/`:** `games/god-of-war-2018/` write-up + NOTES exist. **No `games/god-of-war-ragnarok/`** before this session.
- **Fork `dsvsvd5454-art/coop-anything`:** `gh issue list --search ...` fails because **Issues are disabled** on the fork. `gh pr list --search "ragnarok OR ragnarök OR \"god of war\""` on the fork returned **no matching PRs**.
- **Upstream `cranebeaker/coop-anything`:** `gh pr list --search ...` found merged PR **#239** (`god-of-war-2018: add write-up...`, 2026-10-28). Issue search for the same terms returned **no matching issues** in this session's CLI output.
- **Sibling engine work in-repo:** [games/god-of-war-2018/README.md](../god-of-war-2018/README.md) documents an asymmetric Kratos+Atreus UDP co-op **prototype for the 2018 PC game**, not Ragnarök. Its NOTES explicitly searched for Ragnarök co-op and reported none found as of 2026-10-28.

### External searches (2026-11-10)

Searched (web + GitHub API / `gh search` / Nexus / ModDB):

| Query / place | Result |
|---|---|
| Web: `"God of War Ragnarök/Ragnarok" PC co-op/multiplayer mod` | No co-op mod; Nexus/TheGamer cover single-player mods (FOV, anti-stutter, cheat tables, script loader). |
| Nexus game hub | [godofwarragnarok](https://www.nexusmods.com/games/godofwarragnarok) lists many SP mods (~149 at search time); no co-op project found by name/search phrasing. |
| ModDB mods list | [god-of-war-ragnark/mods](https://www.moddb.com/games/god-of-war-ragnark/mods): **"No mods were found"**. |
| GitHub repos | Script loaders/tools/cheats/hubs (`Eiton/GoWR-Script-Loader`, `iArtorias/smpack`, trainers, landing pages). **No co-op/netplay repo found.** |
| Reddit / Discord | **Not searched directly** this session (tooling / ToS). |

### Observations — existing non-coop tooling (useful later, not a revive target)

- **[Eiton/GoWR-Script-Loader](https://github.com/Eiton/GoWR-Script-Loader)** (MIT, releases `1.0` 2025-03-15, `1.1` 2026-01-08, `1.2` 2026-03-28): `winmm.dll` + `GOWR-Script-Loader.ini` beside `GoWR.exe`; dumps/loads modified scripts without repacking. Required by many Nexus Lua mods.
- **[GoWR MIO](https://www.nexusmods.com/godofwarragnarok/mods/202)** (chris00nexus): `winmm.dll` plugin; Lua + SMS visual-script dump/load, inventory editor, binary patches; claims backward compatibility with Eiton's loader layout (`mod\` paths).
- **Vortex extension** [Nexus site mod 959](https://www.nexusmods.com/site/mods/959): documents Steam/Epic, `exec`/`wad`/`patch`, and Lua under `mod` with an `int9` folder (branch naming aligns with GoW 2018 `int8` notes — **derived**, not verified on disk).
- **Gameplay Lua example:** [Revamped Combat](https://www.nexusmods.com/godofwarragnarok/mods/255) edits `mod/int9/gameart/scripts/characters/heroa00/main.lua` — confirms hero Lua still exists and is injectable.
- **Companion swap (arena only):** [Any Companion (Hrolf Arena Only)](https://www.nexusmods.com/godofwarragnarok/mods/299) — Freya replacement in King's Grave only; **not** multiplayer.
- **Asset tools:** [iArtorias/smpack](https://github.com/iArtorias/smpack) (GPL-3.0), [iArtorias/gowr_soundtool](https://github.com/iArtorias/gowr_soundtool).

### Verdict on "already done"

**No public co-op / multiplayer campaign mod found** to revive. Path is **build from zero**, informed by same-engine GoW 2018 work and Ragnarök script-loader tooling.

## 3. Which engine?

### Observations

- Studio / architecture talks treat the modern SMS engine lineage from Kinetica through GoW 2018 into Ragnarök ([REAC 2024 SMS PDF](https://enginearchitecture.org/downloads/REAC_2024_SMS.pdf)): content in **WADs**, characters as WADs (Kratos, Atreus), Maya-centric pipeline.
- Same PDF: Ragnarök added a **visual script editor "to replace the previous lua-based scripting system"** (also points to GDC 2023 SMS talk).
- This repo's [playbook/engine-families.md](../../playbook/engine-families.md) already lists **Santa Monica Studio Kinetica** with GoW 2018 evidence and names Ragnarök as sibling.
- Nexus/Script-Loader ecosystem still loads **Lua** under `mod/int9/...` for hero/UI-style mods, and GoWR MIO dumps **both** Lua and SMS visual scripts.

### Derived

- Expect a **hybrid**: visual scripts for much level/quest content; Lua still present for character/hero behaviour (and UI), injectable via `winmm.dll` loaders — **not** a full Lua-everywhere match to GoW 2018's 1,423 scripts until we dump an owner's build.

### Unknowns (need install)

- Whether `GoWR.exe` still embeds `socket.core` / `cmsgpack` like GoW 2018.
- Exact Lua version and WAD layout (`exec/wad/pc_le/` etc.).
- SteamStub / multi-instance behaviour on Ragnarök PC.
- How Freya / Atreus companion VMs map vs GoW 2018 `heroa00` / `son00`.

## 4. How much source is there?

| Layer | Status |
|---|---|
| Full engine source / decomp / recomp | **None found** (closed binary PC port). |
| Shipped script source | Not as plain text in install (compiled in WADs); **runtime replace** via Script-Loader / GoWR MIO. |
| Script extender / plugin | **Yes** — public `winmm.dll` loaders (Eiton; GoWR MIO). |
| Open tooling | Script loader (MIT), smpack (GPL-3.0), various SP mods. |

## 5. Does the engine have multiplayer?

### Observations

- Retail game: **no** co-op or multiplayer modes (Game8; PCGamingWiki Modes: Singleplayer).
- GoW 2018 work in this repo found LuaSocket/`cmsgpack` inside that exe — **unknown** whether Ragnarök's exe still links them.
- Older series title **God of War: Ascension** had online PvP; irrelevant as netcode for Ragnarök.

### Derived path if building co-op

- Same rough design as GoW 2018 write-up: **asymmetric companion control** (Kratos host + Atreus/Freya client) is the shortest narrative fit; still requires RE on companion input, sync moves, and story authority.
- Visual-script-heavy quests may be harder than GoW 2018's Lua-heavy path — treat as elevated risk until dumps exist.

## 6. Shipping check

### Observations / derived

- Existing loaders claim **no original game files modified** (`winmm.dll` beside exe; scripts under `mod\`). A co-op mod can ship the same way (DLL + scripts + config), player-owned game required.
- No evidence gathered this session of always-on anti-cheat for the single-player PC build; **unknown** whether any online Sony/Steam overlay feature would conflict — stay clear of any online service abuse per AGENTS.md.
- Do not redistribute game WADs/assets.

## 7. Rough difficulty & triage decision

| Question | Answer |
|---|---|
| Abandoned co-op mod to revive? | **No** (not found by searches above). |
| Same-engine prior art? | **Yes** — GoW 2018 co-op prototype + engine-families notes; loaders for Ragnarök already exist. |
| Path | **`coop-build-from-zero`**, after owner provides install identity and approves claim issue / further tooling. |
| Difficulty | High: closed binary, no shipped MP, visual scripts replace much Lua; mitigated by companion architecture + existing script loaders + GoW 2018 lessons. |

### Guesses (labelled)

- Guess: Atreus segments and Freya companion segments both need separate control maps; Freya may not share GoW 2018 `son00` APIs.
- Guess: `int9` in mod paths is the Ragnarök code branch successor to GoW 2018 `int8`.

### Unknowns blocking Phase 2+

- Owner store, build, SHA-256, install path for a **test copy**.
- Permission to open a **"claim a game"** issue (fork has Issues disabled; needs owner GitHub on upstream or enabling Issues).
- Permission before installing Ghidra/compilers or downloading large tools/game files.
- Discord access if mining modder channels (read [playbook/discord-export.md](../../playbook/discord-export.md) first; ask owner before joining).

## 8. Session log

- `git pull` on `dsvsvd5454-art/coop-anything` — already up to date with `origin/main`.
- Searched directory, `games/`, fork PRs, upstream issues/PRs, GitHub repos, Nexus, ModDB, Steam/PCGW/Blog, REAC 2024 PDF.
- Wrote `games/god-of-war-ragnarok/NOTES.md`, README triage stub, directory gap entry.
- Did **not** download the game, Script-Loader binaries, or install RE tools.
- Did **not** claim co-op works.

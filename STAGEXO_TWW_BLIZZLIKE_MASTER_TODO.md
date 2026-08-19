# STAGEXO The War Within Blizzlike — Master TODO

> Living implementation and validation checklist for `stagexo-the-war-within-1127`.
>
> Baseline commit: `8d31f000f77ff9c2e26d4a31e559943acf4eff03` (`TDB 1127.26011 - 2026/01/14`).
>
> Target expansion: **The War Within**. Initial client/database baseline: **11.2.7**, with auth `build_info` entries through build **65299**.
>
> **Completion rule:** a checkbox is marked `[x]` only after the repository contains the required implementation/data and it has been validated as far as the available environment allows. A script name, placeholder, TODO, partial boss AI, or database row by itself is **not** completion.

## 0. Global project rules

- [x] Keep The War Within work isolated on `stagexo-the-war-within-1127`.
- [x] Base the branch on commit `8d31f000f77ff9c2e26d4a31e559943acf4eff03`.
- [x] Treat the project as The War Within, not Dragonflight.
- [ ] Complete the agreed TWW scope before moving development focus to older expansions.
- [ ] Validate C++ and database changes together for every content milestone.
- [ ] Never invent spell, creature, gameobject, quest, loot, map, encounter, difficulty, currency, or SQL IDs when authoritative data is available.
- [ ] Prefer retail-observed behavior and authoritative Blizzard/client data over custom behavior.
- [ ] Record every completed TWW dungeon, raid, zone, major system, and campaign milestone in this file.
- [ ] Do not mark content complete until normal flow, reset/wipe behavior, rewards, phasing, difficulty logic, and persistence have been checked where applicable.
- [ ] Keep compiler/static-analysis cleanliness as a merge requirement.

## 1. Core / framework baseline audit

- [x] `CURRENT_EXPANSION` is `EXPANSION_THE_WAR_WITHIN`.
- [x] The War Within level cap is 80 in core expansion definitions.
- [x] Auth database baseline contains 11.2.7 build records through build 65299.
- [x] `src/server/scripts/KhazAlgar` exists and is wired through the script loader.
- [ ] Confirm the exact client executable/build we will use for all runtime validation.
- [ ] Validate clean CMake configure on Windows/MSVC.
- [ ] Validate clean full build on Windows/MSVC.
- [ ] Validate clean configure/build on GCC or Clang where practical.
- [ ] Resolve all TWW-related compile errors and warnings introduced by our branch.
- [ ] Run available unit/tests and record failures.
- [ ] Validate `bnetserver` startup.
- [ ] Validate `worldserver` startup.
- [ ] Validate auth/characters/world/hotfixes database creation from clean state.
- [ ] Validate database updater from the baseline full DB to branch HEAD.
- [ ] Validate DB2/hotfix loading for the target client build.
- [ ] Validate map/vmap/mmap data compatibility with the target client build.
- [ ] Validate login, realm list, character list, create/delete/login flow.
- [ ] Audit packet/opcode handling needed by TWW gameplay systems.
- [ ] Audit instance/map framework for TWW maps and difficulties.
- [ ] Audit encounter-state persistence and lockout handling.
- [ ] Audit scenario framework used by campaign, delves, and instanced story content.
- [ ] Audit phasing/conditions/quest objective framework for modern campaign content.
- [ ] Audit spell/aura framework for current TWW class and encounter mechanics.
- [ ] Audit movement/spline/vehicle/transport support used by TWW encounters.
- [ ] Audit personal/warband/account-wide persistence boundaries.

## 2. Current TWW implementation snapshot

### 2.1 Khaz Algar script registration

- [x] Dornogal script is registered.
- [x] Isle of Dorn script is registered.
- [x] The Stonevault instance script is registered.
- [x] E.D.N.A. boss script is registered.
- [x] Skarmorak boss script is registered.
- [x] Nerub'ar Palace instance script is registered.
- [x] Ulgrax the Devourer boss script is registered.
- [x] City of Threads instance script is registered.
- [x] Orator Krix'vizk boss script is registered.
- [ ] Audit every registered script for completeness and retail correctness; registration alone is not completion.

### 2.2 Immediate gaps visible from the script tree

- [ ] The Stonevault — Master Machinists encounter implementation.
- [ ] The Stonevault — Void Speaker Eirich encounter implementation.
- [ ] City of Threads — Fangs of the Queen encounter implementation.
- [ ] City of Threads — The Coaglamation encounter implementation.
- [ ] City of Threads — Izo, the Grand Splicer encounter implementation.
- [ ] Nerub'ar Palace — The Bloodbound Horror encounter implementation.
- [ ] Nerub'ar Palace — Sikran, Captain of the Sureki encounter implementation.
- [ ] Nerub'ar Palace — Rasha'nan encounter implementation.
- [ ] Nerub'ar Palace — Broodtwister Ovi'nax encounter implementation.
- [ ] Nerub'ar Palace — Nexus-Princess Ky'veza encounter implementation.
- [ ] Nerub'ar Palace — The Silken Court encounter implementation.
- [ ] Nerub'ar Palace — Queen Ansurek encounter implementation.
- [ ] Add/verify script roots and loaders for the remaining TWW dungeons, zones, raids, delves, and patch content.

## 3. Khaz Algar leveling world and campaign

### 3.1 Dornogal

- [ ] Audit NPC population, vendors, trainers, services, portals, transports, inn, auction/bank access, and interaction conditions.
- [ ] Audit campaign phasing and post-campaign state.
- [ ] Audit profession and crafting-order integration.
- [ ] Audit renown/faction representatives and reward unlocks.

### 3.2 Isle of Dorn

- [ ] Audit full zone campaign quest chain.
- [ ] Audit side quests and local stories.
- [ ] Audit rares, treasures, events, world quests, and rewards.
- [ ] Audit creature spawns, movement, combat AI, gossip, and phasing.
- [ ] Audit Earthen/Dornogal transition flow.

### 3.3 The Ringing Deeps

- [ ] Add/audit zone script coverage.
- [ ] Audit full campaign chain and scenario transitions.
- [ ] Audit side quests, events, rares, treasures, and world quests.
- [ ] Audit zone phasing and transportation.

### 3.4 Hallowfall

- [ ] Add/audit zone script coverage.
- [ ] Audit full campaign chain.
- [ ] Audit Beledar-related world state behavior.
- [ ] Audit side quests, events, rares, treasures, and world quests.
- [ ] Audit zone phasing and transportation.

### 3.5 Azj-Kahet

- [ ] Add/audit zone script coverage.
- [ ] Audit full campaign chain.
- [ ] Audit Severed Threads progression and related world states.
- [ ] Audit side quests, events, rares, treasures, and world quests.
- [ ] Audit zone phasing and transportation.

### 3.6 Main campaign / max-level campaign

- [ ] Validate campaign chapter ordering and prerequisites.
- [ ] Validate story scenarios and cinematics triggers.
- [ ] Validate account/warband skips only where retail allows them.
- [ ] Validate level-80 campaign unlocks.
- [ ] Validate campaign rewards, currencies, reputation/renown, and item grants.

## 4. TWW launch dungeons

> Each dungeon must be validated for entrance/teleport, instance state, all bosses, trash, scripted events, deaths/wipes/resets, checkpoints, loot, achievements, Normal/Heroic/Mythic behavior, and Mythic+ hooks where applicable.

### 4.1 The Rookery
- [ ] Instance framework.
- [ ] Kyrioss.
- [ ] Stormguard Gorren.
- [ ] Voidstone Monstrosity.
- [ ] Trash/events/loot/achievements/difficulties.

### 4.2 The Stonevault
- [x] Instance script exists.
- [ ] E.D.N.A. — audit existing implementation against retail.
- [ ] Skarmorak — audit existing implementation against retail.
- [ ] Master Machinists.
- [ ] Void Speaker Eirich.
- [ ] Trash/events/loot/achievements/difficulties.

### 4.3 Priory of the Sacred Flame
- [ ] Instance framework.
- [ ] Captain Dailcry.
- [ ] Baron Braunpyke.
- [ ] Prioress Murrpray.
- [ ] Trash/events/loot/achievements/difficulties.

### 4.4 Ara-Kara, City of Echoes
- [ ] Instance framework.
- [ ] Avanoxx.
- [ ] Anub'zekt.
- [ ] Ki'katal the Harvester.
- [ ] Trash/events/loot/achievements/difficulties.

### 4.5 Cinderbrew Meadery
- [ ] Instance framework.
- [ ] Brew Master Aldryr.
- [ ] I'pa.
- [ ] Benk Buzzbee.
- [ ] Goldie Baronbottom.
- [ ] Trash/events/loot/achievements/difficulties.

### 4.6 Darkflame Cleft
- [ ] Instance framework.
- [ ] Ol' Waxbeard.
- [ ] Blazikon.
- [ ] The Candle King.
- [ ] The Darkness.
- [ ] Trash/events/loot/achievements/difficulties.

### 4.7 The Dawnbreaker
- [ ] Instance/ship/transport framework.
- [ ] Speaker Shadowcrown.
- [ ] Anub'ikkaj.
- [ ] Rasha'nan.
- [ ] Flight/ship transitions, trash/events/loot/achievements/difficulties.

### 4.8 City of Threads
- [x] Instance script exists.
- [ ] Orator Krix'vizk — audit existing implementation against retail.
- [ ] Fangs of the Queen.
- [ ] The Coaglamation.
- [ ] Izo, the Grand Splicer.
- [ ] Trash/events/loot/achievements/difficulties.

## 5. Nerub'ar Palace — Season 1 raid

- [x] Instance script exists.
- [ ] Ulgrax the Devourer — audit existing implementation against retail.
- [ ] The Bloodbound Horror.
- [ ] Sikran, Captain of the Sureki.
- [ ] Rasha'nan.
- [ ] Broodtwister Ovi'nax.
- [ ] Nexus-Princess Ky'veza.
- [ ] The Silken Court.
- [ ] Queen Ansurek.
- [ ] Raid Finder wing logic.
- [ ] Normal mechanics/scaling.
- [ ] Heroic mechanics/scaling.
- [ ] Mythic mechanics/scaling.
- [ ] Story Mode where applicable.
- [ ] Trash and pre-boss events.
- [ ] Checkpoints/teleports/doors.
- [ ] Lockouts and encounter persistence.
- [ ] Loot tables and difficulty-specific rewards.
- [ ] Achievements and meta-achievements.

## 6. Delves

- [ ] Audit core Delve/scenario framework.
- [ ] Validate solo and group scaling.
- [ ] Validate companion framework and Brann progression where applicable.
- [ ] Validate tiers/difficulty progression.
- [ ] Validate objectives, checkpoints, deaths, revives, and completion.
- [ ] Validate bountiful/seasonal variants where applicable.
- [ ] Validate keys/currencies/reward chests.
- [ ] Validate Delver's Journey / seasonal progression where applicable.
- [ ] Implement and validate each TWW Delve individually.
- [ ] Track post-launch Delves separately by patch.

## 7. Warbands / account-wide systems

- [ ] Audit Warband Bank storage and permissions.
- [ ] Audit account-wide reputation/renown behavior.
- [ ] Audit account-wide achievements/collections boundaries.
- [ ] Audit Warbound / Warbound-until-equipped item behavior.
- [ ] Audit transferable currencies where supported by retail.
- [ ] Audit account-wide quest/campaign completion flags and skips.
- [ ] Audit cross-character map/exploration/unlock state where applicable.
- [ ] Validate persistence and migration safety.

## 8. Hero Talents / classes / spells

- [ ] Audit Hero Talent unlock and progression framework.
- [ ] Audit every Hero Talent tree for every class/spec.
- [ ] Audit class talent interactions with Hero Talents.
- [ ] Audit proc, aura, periodic, absorb, summon, movement, target-selection, and cooldown mechanics used by TWW spells.
- [ ] Audit TWW class-set bonuses.
- [ ] Audit PvE/PvP spell modifiers separately.
- [ ] Add regression tests for high-risk spell framework fixes where feasible.

## 9. Renown, reputations, world quests, events, and endgame loops

- [ ] Council of Dornogal progression/rewards.
- [ ] Assembly of the Deeps progression/rewards.
- [ ] Hallowfall Arathi progression/rewards.
- [ ] Severed Threads progression/rewards.
- [ ] World quest unlocks, rotations, objectives, scaling, and rewards.
- [ ] Special assignments and weekly activities.
- [ ] Rares, treasures, zone events, and weekly caches.
- [ ] Great Vault TWW criteria/rewards.
- [ ] Upgrade tracks, crests, currencies, vendors, and seasonal caps.

## 10. Professions and crafting

- [ ] TWW profession skill progression.
- [ ] Knowledge/specialization trees.
- [ ] Profession treasures and weekly knowledge sources.
- [ ] Crafting orders / NPC work orders where applicable.
- [ ] Recrafting and optional reagents.
- [ ] Concentration and crafting quality logic.
- [ ] Profession equipment/tools/accessories.
- [ ] Gathering nodes and loot tables.
- [ ] Recipes, discoveries, vendors, and reputation unlocks.

## 11. PvP

- [ ] Deephaul Ravine battleground.
- [ ] Battleground queue and scoring behavior.
- [ ] TWW PvP seasons/reward tracks.
- [ ] Honor/conquest currencies and caps.
- [ ] Rated arena/RBG/Solo Shuffle behavior relevant to the target patch.
- [ ] War Mode rewards/world PvP behavior.
- [ ] TWW PvP item scaling and upgrade rules.

## 12. 11.0.x post-launch content

- [ ] Audit all 11.0.x campaign additions and epilogues present in the target client/data.
- [ ] Siren Isle zone/content.
- [ ] Siren Isle quests/events/rares/treasures/world states.
- [ ] Patch-specific rewards/currencies/items.
- [ ] Patch-specific class/system changes required for 11.2.7 behavior.

## 13. Undermine(d) / Season 2 content

### 13.1 Undermine
- [ ] Zone/map access and hub services.
- [ ] Main campaign continuation.
- [ ] Side quests, rares, treasures, events, and world quests.
- [ ] Cartel progression and rewards.
- [ ] D.R.I.V.E. system.
- [ ] Undermine Delves.
- [ ] Patch-specific currencies/vendors/upgrades.

### 13.2 Operation: Floodgate
- [ ] Instance framework.
- [ ] All four boss encounters.
- [ ] Trash/events/checkpoints.
- [ ] Heroic/Mythic/Mythic+ behavior.
- [ ] Loot/achievements.

### 13.3 Liberation of Undermine
- [ ] Raid instance framework.
- [ ] All eight boss encounters.
- [ ] Raid Finder/Normal/Heroic/Mythic behavior.
- [ ] Story Mode where applicable.
- [ ] Trash/events/checkpoints/lockouts.
- [ ] Loot/achievements/raid progression systems.

## 14. Ghosts of K'aresh / Season 3 content

### 14.1 K'aresh
- [ ] Zone/map access and campaign continuation.
- [ ] Tazavesh hub integration.
- [ ] The K'aresh Trust progression/rewards.
- [ ] Reshii Wraps progression and gameplay integration.
- [ ] Phase Diving.
- [ ] Ecological Succession.
- [ ] Rares, treasures, events, world quests, and patch currencies.

### 14.2 The Archival Assault Delve
- [ ] Scenario/delve implementation.
- [ ] Difficulty/scaling/rewards.
- [ ] Seasonal integration.

### 14.3 Eco-Dome Al'dani
- [ ] Instance framework.
- [ ] Azhiccar.
- [ ] Taah'bat and A'wazj.
- [ ] Soul-Scribe.
- [ ] Trash/events/checkpoints.
- [ ] Normal/Heroic/Mythic/Mythic+ behavior.
- [ ] Loot/achievements.

### 14.4 Manaforge Omega
- [ ] Raid instance framework.
- [ ] Plexus Sentinel.
- [ ] Loom'ithar.
- [ ] Soulbinder Naazindhri.
- [ ] Forgeweaver Araz.
- [ ] The Soul Hunters.
- [ ] Fractillus.
- [ ] Nexus-King Salhadaar.
- [ ] Dimensius, the All-Devouring.
- [ ] Raid Finder/Normal/Heroic/Mythic behavior.
- [ ] Trash/events/checkpoints/lockouts.
- [ ] Loot/achievements/raid progression and renown systems.

## 15. Database integrity audit

- [ ] Establish authoritative source policy for IDs and retail observations.
- [ ] Audit TWW creature templates/spawns/addons/equipment.
- [ ] Audit TWW gameobject templates/spawns.
- [ ] Audit quest templates/objectives/reward data/conditions.
- [ ] Audit spell scripts, spell areas, target positions, linked spells, and proc data.
- [ ] Audit gossip/menu/POI data.
- [ ] Audit SmartAI usage and migrate to C++ only where justified.
- [ ] Audit instance templates/encounter data/access requirements.
- [ ] Audit loot tables and difficulty conditions.
- [ ] Audit vendors/currencies/reputations/renown reward data.
- [ ] Audit transports/areatriggers/scene/conversation data.
- [ ] Audit hotfixes DB schema and VerifiedBuild usage.
- [ ] Ensure every new SQL change has safe forward migration semantics.

## 16. Blizzlike validation standard

For every completed feature/encounter:

- [ ] Retail behavior/source reference recorded.
- [ ] Correct IDs validated from authoritative data.
- [ ] Spawn positions/orientations/phasing validated.
- [ ] Timers and ability cadence validated.
- [ ] Difficulty-specific mechanics validated.
- [ ] Target selection and threat behavior validated.
- [ ] Movement, pathing, evade, leash, and reset behavior validated.
- [ ] Death/wipe/re-engage behavior validated.
- [ ] Dialogue, text, scenes, conversations, and cinematics validated where applicable.
- [ ] Loot/rewards/achievements validated.
- [ ] Database and C++ implementation reviewed together.
- [ ] Compiler/static-analysis risks reviewed.
- [ ] Runtime smoke test completed.
- [ ] Regression impact on older content considered.

## 17. Merge / release gates

- [ ] Clean branch diff with no accidental generated files or unrelated edits.
- [ ] Clean compile on primary Windows toolchain.
- [ ] Secondary compiler validation where practical.
- [ ] Database updater completes without error.
- [ ] `bnetserver` and `worldserver` boot without new fatal errors.
- [ ] Target client can authenticate and enter world.
- [ ] Changed content receives focused runtime validation.
- [ ] No known crash/data-loss blocker remains in the milestone.
- [ ] Master TODO updated in the same branch before merge.

## 18. Expansion order after TWW

> Do not shift primary implementation focus here until the agreed TWW scope above is complete enough to be considered stable/blizzlike.

- [ ] Dragonflight audit and restoration.
- [ ] Shadowlands audit and restoration.
- [ ] Battle for Azeroth audit and restoration.
- [ ] Legion audit and restoration.
- [ ] Warlords of Draenor audit and restoration.
- [ ] Mists of Pandaria audit and restoration.
- [ ] Cataclysm audit and restoration.
- [ ] Wrath of the Lich King audit and restoration.
- [ ] The Burning Crusade audit and restoration.
- [ ] Classic-era world/content audit and restoration.

## 19. First implementation milestone

- [ ] Produce a clean-build validation report for the baseline branch.
- [ ] Audit the complete `KhazAlgar` loader and all currently registered scripts.
- [ ] Audit The Stonevault as the first full dungeon candidate because it already has an instance script and two boss implementations.
- [ ] Verify missing Stonevault encounters and database bindings before writing new code.
- [ ] Implement/fix one encounter at a time with C++ + SQL + validation notes.
- [ ] Update this checklist after every validated milestone.

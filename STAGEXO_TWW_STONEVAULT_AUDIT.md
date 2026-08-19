# STAGEXO TWW — The Stonevault Initial Audit

Branch: `stagexo-the-war-within-1127`

Baseline: `8d31f000f77ff9c2e26d4a31e559943acf4eff03`

Status: **initial source audit only**. Clean compilation, runtime behavior, imported TDB bindings, and retail-mechanics validation are still required.

## 1. Existing source coverage

The dungeon has a dedicated source directory:

`src/server/scripts/KhazAlgar/TheStoneVault/`

Present files:

- `the_stonevault.h`
- `instance_the_stonevault.cpp`
- `boss_edna.cpp`
- `boss_skarmorak.cpp`

The Khaz Algar loader currently registers:

- `AddSC_instance_the_stonevault()`
- `AddSC_boss_edna()`
- `AddSC_boss_skarmorak()`

There are no registered source implementations for Master Machinists or Void Speaker Eirich at this baseline.

## 2. Instance metadata already present

The instance header/source defines:

- Map ID: `2652`
- Encounter count: `4`
- E.D.N.A. encounter data: `2854`
- Skarmorak encounter data: `2880`
- Master Machinists encounter data: `2883`
- Void Speaker Eirich encounter data: `2888`

Boss creature IDs currently defined:

- E.D.N.A.: `210108`
- Skarmorak: `210156`
- Speaker Dorlita: `213216`
- Speaker Brokk: `213217`
- Void Speaker Eirich: `213119`

These IDs are recorded from the existing source only. They must still be cross-checked against authoritative client/retail data before we use them as a basis for new implementation.

## 3. Confirmed structural gaps

### 3.1 Missing encounters

- Master Machinists has data slots/creature IDs but no boss implementation file registered by the loader.
- Void Speaker Eirich has data slots/creature ID but no boss implementation file registered by the loader.

### 3.2 Instance boundary coverage

`instance_the_stonevault.cpp` currently defines a boss boundary only for `DATA_EDNA`.

Before the dungeon can be considered complete, verify/add correct encounter boundaries for:

- Skarmorak
- Master Machinists
- Void Speaker Eirich

Do not invent coordinates. Use retail/client data or verified captures.

### 3.3 Door/progression coverage

Current `DoorData` contains only three doors, all tied to E.D.N.A. state:

- Foundry entrance: open while E.D.N.A. is not in progress
- Door toward Skarmorak: open after E.D.N.A. is done
- Door toward Master Machinists: open after E.D.N.A. is done

No progression/door handling for the later encounters is visible in the current instance script. Full retail route, checkpoints, doors, encounter gating, and post-boss transitions must be audited.

### 3.4 E.D.N.A. intro dependency

The E.D.N.A. intro starts after five creature deaths whose creature StringId is:

`edna_intro_trash`

This creates a hard dependency on world DB data. The repository source audit alone cannot prove the required TDB bindings exist. When the TDB is available/imported, validate:

- exactly which five trash creatures participate
- StringId assignment
- respawn/reset behavior
- whether partial kills survive/reset correctly on wipe/reload
- E.D.N.A. immunity and intro state on fresh instance, wipe, soft reset, and saved instance

## 4. Existing E.D.N.A. implementation

The current source already contains substantial mechanics and should be audited before being rewritten.

Visible implementation includes:

- intro conversation/movement
- Volatile Spike
- Refracting Beam
- Seismic Smash
- Earth Shatterer energy behavior
- Stone Shield-related aura handling
- Mythic/Mythic+ timing branches
- volatile-spike summons/area behavior
- encounter frame engage/disengage
- wipe/death handling

Validation required:

- spell IDs and effect indexes
- target selectors
- exact timer cadence per difficulty
- energy cycle
- Mythic/Mythic+ branching
- spike creation/destruction behavior
- Refracting Beam interaction with spikes
- tank mechanic behavior
- intro sequence and combat activation
- wipe/reset cleanup
- achievement/loot hooks

## 5. Existing Skarmorak implementation

The current source also contains substantial mechanics and should be audited rather than replaced blindly.

Visible implementation includes:

- Crystalline Smash
- Crystal Shards
- Unstable Crash
- Unstable Fragments / Unstable Energy handling
- Fortified Shell
- Shattered Shell
- Void Discharge
- energy-controller behavior
- encounter frame engage/disengage
- wipe/death handling

Validation required:

- energy transitions and timing
- shell absorb stacking/scaling
- crystal visual/absorb selector behavior
- shard placement/count/targeting
- Unstable Energy damage scaling
- Void Discharge start/end conditions
- difficulty-specific behavior
- reset cleanup
- loot/achievement hooks

## 6. Source-quality observations

- Header naming uses `BOSS_SKARMORAX` while encounter/class naming uses `SKARMORAK`; this is not necessarily a functional bug but should be normalized if we touch the header to reduce future mistakes.
- Existing scripts use modern TrinityCore spell validation and scripted spell hooks; do not replace them with ad-hoc AI casts without evidence.
- There are no obvious `TODO` markers in the two existing boss files, so completeness cannot be inferred from TODO comments. Mechanical comparison is required.
- A source file compiling is not proof that required spell scripts, creature ScriptName/StringId bindings, area triggers, or world data are present in TDB.

## 7. Database audit required before implementation

With the actual TDB 1127.26011 world database imported or otherwise available, verify at minimum:

- `instance_template` / map 2652 binding to `instance_the_stonevault`
- boss creature templates and spawn data
- creature ScriptName bindings where required
- `StringId = edna_intro_trash` bindings
- gameobject spawns for the three currently defined doors
- spell script name bindings for E.D.N.A. and Skarmorak
- area trigger create properties/templates/scripts used by both bosses
- conversation/scene data used by E.D.N.A. intro
- dungeon encounter/difficulty data
- loot templates
- creature text / broadcast text
- achievements and criteria
- Mythic+ integration data

## 8. Implementation order

1. Clean compile validation of the unchanged baseline + audit docs.
2. Obtain/query the actual TDB world data for map 2652 and all current script dependencies.
3. Validate E.D.N.A. against retail and correct existing implementation/data.
4. Validate Skarmorak against retail and correct existing implementation/data.
5. Implement Master Machinists using authoritative IDs/mechanics.
6. Implement Void Speaker Eirich using authoritative IDs/mechanics.
7. Complete instance-wide doors, boundaries, checkpoints, trash events, and reset behavior.
8. Validate Normal/Heroic/Mythic and Mythic+ differences.
9. Validate loot, achievements, and end-of-dungeon completion.
10. Mark The Stonevault complete in `STAGEXO_TWW_BLIZZLIKE_MASTER_TODO.md` only after runtime validation.

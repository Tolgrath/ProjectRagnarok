# Project Ragnarok — Design Decisions Register

Last reviewed: 2026-11-22  
Status: Living design record. **Approved** means the player approved the intended game design, **proposed** means discussed but not signed off, and **implementation / testing** is tracked separately. No listed feature should be represented as shipped solely because it is approved here.

## Repository and reference conventions

- Public website: https://tolgrath.github.io/ProjectRagnarok/
- Official release changelog: GitHub Releases; the website Dev Log reads release notes automatically.
- Local game project (Codex): `G:\Project Ragnarok\Godot Project`. The public website repository is not the Godot game source.
- Local design reference folder: `G:\Project Ragnarok\Design Assets\Visual References`
- Visual files confirmed saved by player:
  - `base_character_models_ reference_sheet_default_human` (exact extension may vary)
  - `ui_reference_pack_ingame_screen`
  - `menu_reference_pack_full_menu_concepts_inventory_character_party_build_journey_map`
- These local reference files are **not currently available as site assets**. Do not present approximate diagrams as exact copies of approved references. Codex should inspect the originals locally.

## Approved: Art direction & character models

- Stylized, appealing full 3D game art; approved base male/female character reference is the definitive visual target and should remain consistent across classes and four body archetypes.
- Character starting appearance: basic undergarments only; equipped clothing is separate. Models and previews must match across creator, world, menus and co-op.
- Female direction: attractive expressive face, fuller bust, defined waist, shapely hips/glutes, strong thighs. Male direction: rugged attractive face, powerful shoulders/chest/arms/back/legs.
- Characters need naturally relaxed idle animation rather than rigid mannequin poses; improve breathing, posture, shifts and animation transitions with performance-conscious skeletal animation.
- Close gameplay camera zoom previously tested and approved; preserve approved movement/combat/cursor behaviour.
- Character creator set in a tasteful low-cost Viking timber bathhouse/dressing area, character on **right**, wizard choices on **left**, feet fixed in world space. Player can rotate, pan, reset and cursor-focused zoom to **any** body region, not only preset locations.
- Do not mistake a rendered concept for an importable 3D mesh. Artistic quality and technical integration require separate validation.

## Approved: Character creation, world ownership and TP

- A survivor belongs to their world; create or choose the world first, then create its survivor.
- First survivor wizard: **World → Class → Body → Appearance → Finalize**.
- Successor wizard after permanent death: **Class → Body → Appearance → Transference Points → Finalize**. No world recreation, no resetting the persistent settlement/world or surviving co-op players.
- Wizard options are revisitable; going backwards retains selections until final confirmation.
- Transference Point allocation is provisional while editing. Allow allocating, undoing and redistributing points, and show available/remaining TP and costs. **Commit atomically only at successful Finalize**; cancel/exit cannot consume TP, duplication or overspending must be prevented.
- TP is world-specific progression and distinct from the separate class/occupation unlock progression. Exact class unlock thresholds are not defined in this record.

## Approved: HUD, menus and interaction

- Primary UI black/near-black with medium-grey borders, subtle accents, high readability, very little ornamentation, and ~10–20 px screen-edge margins at reference size.
- **Bottom-left:** compact standalone health, stamina, thirst, hunger bars. **No enclosing background or border panel.**
- **Bottom-centre:** compact 10-slot hotbar (1–0), centred item images taking ~95% of icon area; quantities only for stackable items, bottom-right of slot; hotkeys centred underneath.
- **Bottom-right:** six compact menu icon buttons (about half hotbar-slot size), each with only its hotkey underneath: **Inventory I; Character C; Party P; Map M; Build B; Journey J**.
- **Top-right:** area name, compact minimap, digital time, illustrated changing time-of-day (dawn/day/dusk/night), subtle tracked quest below. No facing-direction, resource-total, infected-count or global hotkey legend clutter.
- Rename Pack → Inventory; Survivor → Character. Menus should have distinct coherent layouts rather than one generic data-heavy window.
- Interaction label appears above one currently eligible interactable NPC/bench/campfire/object **only within ~1–2 metres**, with centered two lines: **name** and **[F to interact]**. Billboard toward local player camera; one active prompt and exact matching F target per player. Stable target preference to prevent flicker when several objects overlap.
- Opening UI automatically releases mouse; closing restores gameplay cursor capture; ESC closes topmost menu first.

## Approved: Inventory / Character / Party / Build / Journey / Map

- Inventory: icon grid, genuine item/stack quantities, equipment/hotbar management, item details and existing crafting/storage integration.
- Character: real full-body preview, equipment slots, existing stats, conditions and progression; no invented data.
- Party: human co-op members clearly distinguished from NPCs, status/roles/orders, real functional commands; animal companion support planned but not falsely displayed as implemented.
- Build: category selection → **icon grid for individual blueprints**, not another dropdown. Large preview and requirements shown by resource **pictures** and centred **have/need** counts (e.g. `5/10`), not text-only recipe lists. Placement help appears only during placement mode, never on Build menu.
- Journey: main / side / active / completed quests, detail, objectives, relevant rewards, tracking and real HUD sync.
- Map: terrain revealed in smooth **radial proximity** around the player; underlying grid/storage may be optimized but visual fog boundary should not appear as hard square blocks. Previously discovered terrain persists. Undiscovered POIs are hidden from map/filters/labels. Quests can reveal approximate **search radius**, never exact undiscovered POI position. Discovering the POI reveals the exact marker.

## Approved: Wildlife and animal companions — future systems

- No dragons/trolls/fantasy monster roster in the initial creature scope. Focus on Viking-era wildlife, livestock, functional companions and infected animals.
- Performance-sensitive, species-specific behaviour: prey senses/grazing/fleeing; predators hunt, investigate, avoid danger, defend, retreat; healthy predators can hunt other creatures when within actively simulated area.
- Near creatures use full relevant AI; distant wildlife uses reduced tick rates and far-away lightweight/abstract state, not continuously expensive full simulation.
- Companion animals do more than follow/attack: bonding, useful roles, training and commands. Ordinary domesticated livestock should not run fully capable companion AI.
- Companions **can contract the plague, be treated and recover**, retaining their established bond and training on successful cure. Animal treatment follows approved human infection progression rules with anatomical implications, including potential limb amputation where applicable. Reanimation after death follows existing plague rules. No immediate hostility merely because infection begins.
- Plague-stage game rules already approved: 0–35% early herbs; 36–60% stronger herbs/care; 61–85% limb amputation where possible; 86–100% no cure and eventual death/reanimation. These are game mechanics, not medical advice.
- Infected animals retain natural physical capabilities but lose normal healthy survival behaviours as specified; infected wolves lack healthy pack tactics. Spread requires direct infected bodily-fluid transmission; raw meat only risky if its animal was infected at kill.

## Previously approved systems — preservation constraints

- Persistent world/settlement and succession on death; world-specific TP; death procession / memorial and recoverable physical belongings; world-specific Memories screenshot/album and co-op sharing rules.
- Movement: WASD; mouse-driven free camera; RMB forward-facing strafing; LMB attack; no permanent crosshair; F for interact; automatic cursor release on menus.
- Do not regress save compatibility, multiplayer player isolation, equipment and building functionality, performance, or local screenshots.

## Planned roadmap (provisional; not a feature-completion claim)

- v0.16: UI/visual foundation & integration
- v0.17: Living wilderness
- v0.18: Functional companions and husbandry
- v0.19: Animal plague behaviours and treatment
- v0.20–v0.25: deeper settlement, survival, exploration, combat, legacy, co-op polish and integration. **Exact version assignments remain subject to review.**

## Implementation and release status

- v0.14 and v0.15 Alpha Playtest prereleases exist on GitHub. The v0.15 work described in design discussions and Codex reports is **not automatically verified or officially signed off**.
- Codex screenshots showed UI and menu functional foundations, but multiple art and layout deficiencies remain; new creator wizard, radial fog and TP workflow are part of a subsequent Codex instruction, **not confirmed implemented**.
- Current game model and animation quality requires direct in-game inspection, separate from artistic reference approval.
- Public site Dev Log is release-based and must not report draft design choices as shipped changes.
- No official publish without a user playtest and approval.

## Maintenance protocol

1. When the user approves a new design decision, add it to this register under the relevant **Approved** section.
2. Keep **Proposed / needs discussion** ideas separately and do not silently upgrade them to approved.
3. Record what Codex says was implemented separately from what has been verified through actual playtesting.
4. On official user-approved release, write structured **Added / Changed / Fixed / Known Issues** GitHub Release notes. The website Dev Log will display them automatically.
5. Preserve approved artwork as separate files with accurate names and licence provenance; avoid overwriting the reference sheet or reinterpreting it as a game-ready asset.
6. The live site notes are a curated digest of this file, not a substitute for the full decision history.

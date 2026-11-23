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
- Public prereleases may be published at the user's explicit direction for testing; do not misstate them as fully verified or stable. User acceptance and two-PC verification are separate release checkpoints.

## Published release checkpoint — 2026-11-22

- **Published by the user:** [Project Ragnarok v0.15 — Co-op Alpha Playtest](https://github.com/Tolgrath/ProjectRagnarok/releases/tag/v0.15-coop-playtest), tag `v0.15-coop-playtest`, Windows ZIP `ProjectRagnarok-v0.15-Windows-Coop-Playtest.zip` (66,682,400 bytes).
- **Package SHA-256 reported by Codex (not independently rehashed here):** `680013363EED5ED76F99A5EB57BDAC38C1CD466516B05A31922D69BA187CF75A`.
- The release notes list the **open-air washing/dressing area**, two Viking figures incorporated **into the static background artwork only** (not 3D NPCs), menu/tab polish, improved finalization summaries, corrected body/appearance consistency and female presets clearing beard selection.
- **Reported Codex validation:** 21 local host/guest checks, 8 shared-stock checks, 161 prototype regressions, and extracted Windows executable launching main menu, creator and forest.
- **Still awaiting user verification:** physical two-PC LAN co-op and any packet-loss / real-network issues; in-world visual parity with approved character reference remains incomplete.
- The earlier `v0.15-playtest` and `v0.14-playtest` remain preserved. This is a new tagged prerelease rather than an overwrite.
- Website main gated download was changed to this exact published ZIP; the automated Dev Log shows the release's GitHub patch notes.

## Two-PC field test recorded — 2026-11-22 (open items)

- The user and a friend **tested the published co-op alpha on separate PCs**. This changes prior status from *physical testing not performed* to *performed with significant defects*. It does **not** mean two-PC co-op passed.
- The user reported **59 numbered observations, defects, questions and proposals**. Full original-language ledger: [v0.15 Two-PC Playtest Findings](v0.15-two-pc-playtest-findings.md).
- Highest-priority observations: guest lag, guest food/water glitching, lack of TP distribution on succession, only one TP choice for both host/guest, guest trophies and tree gathering, broken large boulder mining, broken storage chests, unexplained high fever/severe illness/weakness.
- Next build recommendations: reproduce/network-log before claiming root cause; validate actual two-client host/guest state rather than relying only on loopback test counts; fix existing mechanics before expanding fauna or world dimensions.
- Additional **user requests and reports awaiting design/implementation**: delete worlds; improved death message; left-hand fingers; creator/hosting/joining flow; host player count arrows; guest spawn; player feedback on hits and TP; structure rotation/snapping; stamina tuning; inventory drop/context menus; berries supply water; death-item auto-gather prohibition; Procession of Fallen; NPC base commands; ammo; survival bar warnings; x-ray occluders; minimap center; more animals/enemies; bow aim; tombstone removal; beds purpose; settlement cap; map size/terrain; palisade gate; handedness/offhand; sounds/audio settings; responsive UI; rain weather/collector logic; trusted Windows signing and updater/launcher investigation.
- These are **field findings and requested directions, not yet fixes or independently confirmed implementations**. Where a question asks about current code (map size, NPC cap, beds, illness trigger), the answer requires inspecting the local Godot project.

## Approved for next authorized build — 2026-11-23

- **New gameplay specifications approved today:** tiered forage resources and stack limits, breakdown tools/stations, exact starter tool/weapon/ammunition recipes, permanent dedicated non-combat tool slots with in-place upgrades, realistic resource yields, wound/bleeding rules, plague-only infection, food poisoning and medical crafting.
- **Authoritative detailed specification:** [Next-build crafting, tools & medical spec](next-build-crafting-tools-medical-spec-2026-11-23.md). Read this **before Codex implementation**. Latest user corrections take precedence over older inconsistent recipes and ailment notes.
- **Tool/weapon roster locked:** Do not add any weapon or tool without explicit player instruction. Tools are non-combat, have no durability, occupy their own permanent category slot, are never duplicated/stored as spares, are automatically drawn for relevant actions and upgraded in place.
- **Medical bleed rule:** one bleeding type per wound, normal 2 HP/s or severe 3 HP/s until treated. Basic wrap only temporarily suppresses severe bleed for 60 seconds; it does not heal the wound.
- **Plague only:** infected-wound stages refer to the zombie plague, not ordinary wound infections. Food poisoning causes hunger/thirst to drain at 110% of existing base; base rates must be measured from actual code.
- **Implementation status:** design documented, not coded/published. Integrate with v0.16 local candidate and preserve ongoing co-op recovery; next build requires explicit user authorization.

## Requested world, combat and wildlife milestone — 2026-11-23

- **Newly requested:** sea-surrounded island with a map size increase of 50%, at least one river, ravens/rabbits alongside deer/wolves/boars/bears, at least two class-dependent reanimated survivor versions and reanimated animals, less restrictive camera pitch, separate ranged aim calculation and RMB facing-lock crosshair for both melee/ranged attacks, tree/boulder auto-gather, more rebindable controls, crouch/sneak, and functional single-player Procession of the Fallen.
- **Deferred for later discussion:** animal-hide pouches to increase item-specific carrying capacities, inspired by The Forest; no mechanics or recipes approved yet.
- **Implementation status:** requirements recorded, not implemented. Detailed [world, combat, wildlife & controls request](next-world-combat-wildlife-requirements-2026-11-23.md).
- **Size ambiguity:** 50% more linear dimensions and 50% more total area yield different map sizes. Do not mark a numeric size finalized until interpreted with the user.
- **Restrictions:** no independently invented tools or weapons; preserve existing 3D project, save compatibility and the current preference for mostly solo tests.

## Solo field feedback — revised v0.17 island candidate (2026-11-23)

**User-observed, still open:** These findings are from a quick solo playtest of the revised local v0.17 candidate. They are not fixed or user-approved as implemented.

1. **Release updates:** User requests an easy automatic updater, potentially a main-menu "New update available — click to update" notification that downloads and restarts. Feasible design: lightweight external updater process to replace the running Windows EXE safely; check user-approved published GitHub release assets, verify source and SHA-256 or signature, stage download, back up existing files, close game, atomic swap/rollback, restart, preserve saves/settings outside installation directory, show errors/progress and provide offline/manual fallback. Avoid automatically installing every prerelease, including untested candidates. This is a proposed implementation, not yet approved.
2. **Auto-gather bug:** Held auto-gather omits plant fibre and cobble. Audit forage registry and harvesting routing for these exact resources and protect dead-survivor items from auto-loot.
3. **Keybinding UX:** User calls current binding interface "terrible." Rework readable action grouping, key capture prompts, conflict checks, reset defaults and saved bindings; do not assume a particular layout was approved.
4. **Crosshair quality:** RMB reticle functions but is very jerky. Diagnose raw mouse input, interpolation, aim elevation vs camera mode handoff and frame-time jitter. Improve smoothness without hiding actual aiming error or adding excessive latency.
5. **Inventory sorting:** Add functioning inventory Sort button preserving stacks, quantities, hotbar references, ownership and multiplayer authority; sort order is not yet specified.
6. **Death procession UI:** Position death message immediately above bottom hotbar instead of blocking the procession; test responsive layout and scaling.

**Development process:** solo testing is primary; physical two-PC testing roughly every other weekend. Do not interrupt or overwrite current candidate; incorporate in next authorized update. No public release or website mutation implied by this feedback.

## Approved corrections — auto-gather, menus and infection-death procession (2026-11-23)

**Status:** User-approved gameplay and presentation requirements for the next authorized 3D build; **not yet implemented or tested**. The following corrects and supersedes narrower v0.17 solo-test notes. Do not modify the current packaged candidate, public GitHub Release or website as part of documentation.

### Automatic gathering
- Auto-gather should **prioritize eligible resources lying on the ground over harvesting trees and boulders**. When no higher-priority eligible ground resource is nearby, proceed to trees/boulders with the correct permanently equipped tool.
- **Include every eligible naturally spawned resource lying on the ground**, not only plant fibre and cobbles; keep stack limits, inventory capacity, interaction distance, resource depletion and authority rules.
- **Exclude any player-dropped resource/item for 60 seconds after being dropped**. This exemption prevents immediately picking up deliberately dropped items; ensure an authoritative drop timestamp rather than an exploitable client-only timer. Eligible once the 60-second window has elapsed.
- **Include animal carcasses** in auto-gather/harvesting, checking for an eligible equipped harvesting knife and correct species loot/treatment rules. A carcass is not the same as a dead survivor's grave or belongings.
- **Never auto-gather player/survivor corpses, grave loot or dropped belongings from dead survivors**, even after 60 seconds; these need deliberate interactions under existing memorial/recovery rules.
- Preserve co-op ownership and prevent simultaneous auto-gather duplication.

### Menu UI
- **Remove dropdown menus across the entire game UI**, including Settings, creator, inventory/crafting and other menus. Replace with appropriate visible alternatives (tabs, buttons, icon grids, segmented choices, lists, or increment/decrement controls) that can handle existing options.
- Maintain all settings/character data and accessible keyboard/mouse navigation. Do not sacrifice screen scaling or functionality for a flat layout. Related feedback: key rebinding is particularly poor; redesign capture, conflict warning, defaults and saved controls without dropdowns.

### Procession of the Fallen — visuals and conditional death rules
- **Four mysterious spectral figures** carry a normally deceased survivor's corpse **at shoulder height** throughout the procession.
- Clothing should move and flow convincingly during walking; figures are ghosts and should be **slightly transparent** (not invisible). Keep performance manageable.
- **If survivor dies because of plague infection:** do **not** initiate a procession immediately. Survivor reanimates as a roaming infected Viking retaining an identity link to that fallen survivor; use approved infected movement/behaviour rules.
- **Only once that reanimated survivor is killed** should the four-figure procession occur and the fallen survivor be honoured. This creates a gameplay objective to find and put down the former survivor; do not add an automatic timeout procession or silently honour them while infected.
- **Immediately upon infection death:** notify settlement/village of the fallen survivor. Show **an unmarked grave**, with the survivor's belongings visibly laid **in front of it**. The grave is not yet a full memorial/honour. Ensure unmarked marker, loot, infected former survivor and later procession/memorial are consistently linked, survive save/reload, and cannot duplicate or lose possessions.
- The unmarked grave is a placeholder of loss, not proof the roaming infected body has been laid to rest. When the reanimated former survivor is put down, transition to the proper procession and honouring flow without duplicate graves or loot.
- Continue to support the already approved **single-player** procession; do not require guest/NPC player presence. Reconcile settlement and no-settlement fallback rules with this exception.
- Do not alter the separate rules for plague infection and limb treatment, ordinary non-infection death, or tool/weapon roster.

### Open implementation details (not yet gameplay decisions)
- The exact sorting among multiple eligible ground pickups/animal carcasses and handling inaccessible targets may use stable nearest-reachable targeting, but should not spin or constantly retarget.
- How the unmarked grave transitions to a completed memorial and how corpse/loot recovery interacts with the plague reanimation should preserve existing death, succession and recovery semantics; use documented consistent behaviour and flag any genuine conflict.
- Animating four semi-transparent carriers at shoulder height is required visually, but may be achieved with lightweight shaders/animation rather than expensive real-time physics; evaluate in-game from more than one camera angle.

**Next-build acceptance:** solo manual checks of priority ground→tree/boulder, 60s no-repickup, animal harvesting, no survivor auto-loot, dropdown-free UI, ordinary death procession, infection death→roaming infected plus unmarked grave and settlement notification→former survivor defeat→spectral procession, and save/reload in both death branches. Physical two-PC testing stays a separate pending validation.

## Maintenance protocol

1. When the user approves a new design decision, add it to this register under the relevant **Approved** section.
2. Keep **Proposed / needs discussion** ideas separately and do not silently upgrade them to approved.
3. Record what Codex says was implemented separately from what has been verified through actual playtesting.
4. On official user-approved release, write structured **Added / Changed / Fixed / Known Issues** GitHub Release notes. The website Dev Log will display them automatically.
5. Preserve approved artwork as separate files with accurate names and licence provenance; avoid overwriting the reference sheet or reinterpreting it as a game-ready asset.
6. The live site notes are a curated digest of this file, not a substitute for the full decision history.

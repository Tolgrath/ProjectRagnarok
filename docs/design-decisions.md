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

## Approved consolidated v0.17 follow-up / Fallen Champion and drop UX — 2026-11-23

**User authorization:** Prepare a Codex instruction now incorporating this material and the previous reported solo-test fixes. Implement in the *next local v0.17 revision* from the latest source snapshot; back up first, maintain v0.16/v0.17 archives and saved games. Do not publish new release/site without user approval.

### Item visuals and dropped-item sacks
- Audit **all registered inventory items** (including legacy and newly added items). Generate **an appropriate distinct, recognizable game-style icon for each item currently using a default/placeholder icon**. Reuse icons that are already good. Do not simply recolor one shared silhouette; map icons correctly by item ID, legible at actual UI size, with consistent style and efficient texture loading. If art-generation capability unavailable in Codex, use genuinely distinguishable authored/procedurally rendered icons and document quality limits; do not claim unique art that isn't there.
- Instead of loose dropped-object models, player item drops should appear as **a burlap sack**. Multiple items dropped **within 2 metres** of an existing drop sack should go into that sack's stored inventory rather than spawning another sack. Preserve item IDs, quantities, stacks, location and ownership, inventory space, co-op authority, saving/loading and object cleanup. If no sack is nearby, spawn one. Allow deliberate interaction to inspect/retrieve contents. **Auto-gather must not pick up newly player-dropped items for 60 seconds**, including if contained in a sack; never auto-loot corpse/grave belongings. Prevent drop-and-repickup infinite loops and duplication.

### Fallen Champion — new explicit design over previous generic reanimation
- If a player survivor dies **because of plague infection**, no immediate procession; an infected Fallen Champion retains that survivor's original name, class/playstyle, achievements, visual identity and power snapshot at moment of death. **Only that former survivor's progression determines boss scale and power**; successors never cause it to scale further.
- Title format: **“[Survivor Name], the Fallen [Archetype]”** (e.g. “Tolgrath, the Fallen Berserker”). Choose archetype based on former playstyle, not successor.
- Size **1.5× default/minimum to 2.5× maximum** of normal Viking height, scaling with fallen survivor achievements. Animate/collide accordingly; recognizably retain former Viking identity. The encounter must be appropriately challenging but not unfair.
- The boss has an encounter site **near its place of death** and eventually **petrifies/dormant as a colossal statue** there; do not leave it freely roaming and vulnerable to random villagers killing it. This supersedes earlier generic persistent roaming for player former-leader champion encounters, without altering ordinary infected survivors/NPCs. No random NPC or wildlife should accidentally awaken or kill it.
- Inactive statue remains an environmental mystery even before quest. Intruders who are **not authorized/ready to awaken it** hear exact voiced or text-backed line: **“Only ye who are worthy may crack the stone that binds thy fate!”** Don't require voice synthesis; text/subtitles and ominous audio are acceptable pending actual voice assets. Exact trigger of readiness beyond successor/quest may follow safe default and be clearly reported.
- In boss area: **progressive ominous darkening**, eerie background audio/music transition, cracked stone, faint plague seams/glow, ravens, corrupted ground, dust and low rumbling; restore regular lighting/music smoothly on exit; avoid expensive whole-world rendering changes. When eligible successor approaches/engages, statue cracks and boss awakens.
- Boss fighting styles reflect former player's dominant fighting approach: **melee**→uses large tree trunk as boss-only environmental attack prop with telegraphed swings/slams; **ranged**→throws nearby environmental objects; endurance/defensive→strong physical slams/counters is a possible archetype. The existing normal infected rule of no traditional weapons/tool use still applies; these are special boss-only physical/environmental attacks, no new player-usable weapon or tool. Clear attack windups, hitbox fairness, leash and reset; don't let it destroy villages.
- Successor appears **on the outskirts near the village** (not distant random location). A **senior/high-level NPC** offers quest *Slay the Fallen Champion*, recognizing the new survivor's promise **without assuming a family/identity connection or automatically recognizing their leadership**. User's proposed flavour line: “I see our leader in you, you have the potential of greatness... but one thing stands in your way. Bring peace to our former leader, who suffered a most awful fate, and his people will follow you! Slay the Fallen Champion!” Polish grammar only if consistent with intent.
- During infected-form interval the village gets a death notice and shows **unmarked grave** with former survivor's loot **in front**; no proper honours until boss defeated. Maintain no duplicated corpse or loot as model transitions to stone/awakens/dies. On boss defeat, trigger the **four-ghost Procession of the Fallen**, honour deceased, progress quest, and earn back village trust; both quest order and pre-quest environmental discovery should be handled.
- Normal non-infection death uses the existing procession with **four slightly translucent ghosts carrying the corpse at shoulder height, flowing garments**, death message just above hotbar. **Original, airy, solemn ghostly music** during processions, especially poignant after boss defeat; use licensed/owned audio or original composition, no unlicensed commercial assets.

### Previously approved same-cycle fixes
- Ground resources prioritized above tree/boulder, gather all eligible ground resource kinds, harvest animal carcasses with dedicated knife, exclude player drops for first 60s, never auto-harvest dead survivor loot, preserve host authority.
- Eliminate **all dropdown menus**; replace with clear tabs/buttons/grids, redesign key rebinding with clear action/primary/secondary, conflict detection, saved mappings, restore defaults.
- Fix jittery RMB crosshair/mouse-aim separately from camera, without adding aim lag; maintain accurate bow/sling/javelin.
- Add functioning player inventory sort controls (respect stacks and hotbar bindings and network sync).
- User wants easy game updating: main-menu update notification and one-click secure download/restart using a **separate helper**, approved-published GitHub Release assets only, integrity verification, backup/rollback and save preservation. No auto-install of unapproved development candidates; don't build new launcher unless needed.
- All changes must retain resource/crafting/wounds/medical specs and the locked player tool/weapon roster. Hide-capacity pouches remain a **future-only idea**, not part of this build.

**Testing and deliverables:** real Godot/Windows candidate, versioned rollback snapshot, unit and in-engine validation incl. infection death→statue→quest→battle→funeral, solo pre-quest mystery, 60s timed sack behaviour, inventory consistency/save-load, performance and network compatibility fixtures; acknowledge physical two-PC tests not yet done. Supply local path, release notes, test report, screenshots, checksum and known limitations. Avoid publishing publicly until user approves.

## Solo playtest feedback — inventory, resources, water, combat and world management (2026-11-23)

**Status:** User-requested changes and observations; open for the **next authorized** 3D Godot implementation. No claim of completion. Preserve the last candidate, backups and existing saves.

### Inventory, equipment and hotbar
- Once **armour or shields are equipped**, they must **stop occupying backpack/inventory slots**. Unequipping should restore the item safely to an available inventory slot, or be refused clearly when full. Inventory count, equipment persistence and host/guest ownership must remain accurate. Clarify whether separate armour slots exist by inspecting code; do not destroy items.
- **Increase berry stack limit** (currently 8 in v0.17 catalogue), exact new cap not specified; choose a sensible cap for discussion or confirm it before implementing. **Increase spring water / raw_water stack limit** (currently 8), exact new cap not specified. Keep clean water distinctions explicit.
- On death/successor recovery of possessions, **restore items to their original hotbar slots** where possible, rather than merely returning them to backpack. Preserve recorded slot mapping across death, procession, Fallen Champion, save/reload and network. Handle occupied slots predictably and without loss.
- In inventory UI, **remove hotbar scrolling** and **shrink hotbar by 15%** compared to its current inventory-screen size; keep gameplay hotbar unchanged. Display **item quantity** on hotbar slots in inventory view, matching actual stacks.

### Resources, harvesting, auto-gather
- **Only harvesting knives can harvest animal bodies**; no bare-handed harvesting or other tools.
- **Only explicitly user-approved resource types should appear in newly generated gameplay/crafting.** Generic legacy `stone` is **not** approved, nor are other unsupported legacy-resource recipes. Audit legacy resource items, resource spawners, collection rewards, crafting/building recipes and inventory compatibility; make new content adhere to approved tiered resources (pebbles/cobbles/stone slabs, sticks/branches/logs, etc.) instead of stone/wood stand-ins. Never casually delete or corrupt old saves; inventory migration/compatibility needs careful reporting. Do not interpret removing `stone` as removing legitimate approved stone-based weapons or the tiered cobble/slab items.
- Auto-gather pathfinding must become **smarter and reliable**: avoid obstacles, unreachable targets, rapid target switching, path loops; preserve ground > carcass > tree/boulder priority, tool prerequisites, 60s newly dropped exclusion and prohibition on automated grave/corpse loot.
- Add **Options → Auto-Gather** with **individual opt-in/opt-out checkboxes for each eligible item/resource category**, persistent per profile/survivor as appropriate; ensure defaults match approved auto-gather and never introduce auto-looting forbidden memorial items.

### World, collision, water, animals
- Add **lightweight buoyancy/flotation** and **basic swim animations**, applying water physics consistently to **all creatures** (players, NPCs and animals), with sensible movement transitions at waterlines and ford/sea/river. IMPORTANT previous plague design states **infected cannot swim, sink and thrash**. This request for physics on all creatures may include infected water interaction, but is **not sufficient by itself to silently grant infected swimming ability**; implement physical sinking/thrashing for infected unless user explicitly revises that rule.
- Add reliable collision volumes to **POI structures** and verify the survivor cannot walk through solid walls, pillars, roofs or other relevant geometry. Avoid blocking functional entrances or AI routes.

### Procession of the Fallen
- Four spectral carriers exist but **they appear to fly**. Correct locomotion and body transport: feet at ground level, grounded walking/gait and foot placement over terrain, actual shoulder-height corpse carry, light translucent ghost clothing and flowing movement. No floating procession except an explicitly designed separate no-ground fallback. Preserve music and solo funeral.

### Combat and medical
- **Aiming remains inaccurate.** A projectile should **strike the surface or target indicated by the crosshair** when unobstructed, using correct crosshair-to-world ray/camera-to-muzzle aim solving and projectile collision. Address origin obstruction/ballistics honestly where trajectory is physically impossible, rather than knowingly displaying a misleading hit reticle. Test across pitch, range, terrain, moving targets, and native frames, retaining RMB facing lock.
- **Severe bleeding feels excessively aggressive** in solo test. Existing locked approved rule: severe **3 HP/s per severe wound**, normal **2 HP/s per normal wound**, one bleed class per wound and 60s temporary basic wrap. **Do not silently change these approved numeric rates.** Audit damage application for double ticks, multiple duplicate wounds, frequency, double counting or missing timer suppression; report whether observed aggression is correct-by-spec or a defect. Propose any balancing adjustment separately for user decision.

### Progression and world management
- **Assess passive skills purchasable with TP**: audit existing skills, prices, scaling, availability, missing benefits, power balance, descriptions and whether they actually affect character stats. Report findings and recommended refinements before assuming numerical rule changes are approved.
- Add **Delete World** option to world selection with clear name/seed confirmation and preferably recoverable trash/backup; prevent accidental deletion of active/shared worlds, delete only the chosen world, preserve other saves/profiles/settings, and handle errors.

### Verification / delivery
- Test actual native Windows interaction and full save/load; no slot/item loss, infinite resource spawns, illicit harvest, water softlocks, POI clipping or accidental world deletion. Keep honest solo vs co-op status. No public release or website claim of implementation until validated and approved.

## Latest corrections / confirmed next-build rules — 2026-11-23 evening

**Status:** User-approved corrections to the open v0.17 feedback. Not yet implemented. These **supersede conflicting earlier statements**.

- **Berries:** max stack **100** (was 8).
- **Spring water** (`raw_water`): max stack **100** (was 8). Do not silently conflate this with `water` (clean water) unless separately approved.
- **No backward save compatibility requirement at this development stage.** Previous saves can be discarded; remove legacy items/registries/recipes instead of retaining unsupported resources merely to protect old saves. Continue using isolated test saves and preserving current project backup for development safety.
- **Approved resource whitelist** comes from [2026-11-23 crafting/medical specification](next-build-crafting-tools-medical-spec-2026-11-23.md): stick, pebble, plant_fibre, bark, leek, mushroom, bone, branch, cobble, log, stone_slab, plus expressly approved crafted resources such as tog, and separately approved animal yields, food, medical items, weapons, armour and equipment where established. **Generic `stone` is forbidden**. Also audit unspecified/legacy `wood`, `plank`, `supplies`, `dressing`, `clean_bandage`, `wound_wash`, duplicate historical equipment, and all other entries against *actual* express user approvals, not the existing registry as authority. **Remove field dressing** (`dressing`) specifically. Do not introduce replacements unapproved by the user. If removal breaks POI building, combat, crafting or quests, rework dependency to explicitly approved ingredients or identify the blocked recipe instead of silently inventing new quantities. Do not interpret stone weapon descriptors as the forbidden generic stone resource.
- **Water:** minimal buoyancy/flotation and swim animations/physics for healthy survivors, NPCs, animals; **infected remain unable to swim**, sink and thrash, per locked original rule. Water has physical interaction for infected, not swimming competence.
- **Procession:** the **Grim Reaper LEADS** the procession. The four translucent ghostly bearers remain and must **walk on the ground**, carry the body at shoulder height with flowing clothes. Reaper is a distinct lead character, not a substitution for one of the four bearers. Keep eerie airy original funeral music.
- **Target outline:** when crosshair *actually targets an enemy that the shot is expected to hit*, show a **basic red silhouette/outline** around that enemy. Do not mark a blocked/occluded enemy or pretend a projectile will hit it when actual trajectory/collision disagrees. Aim must hit the crosshair target when physically possible; test raycast/camera muzzle, ballistic travel, target movement and UI timing.
- **Severe bleeding:** user reports dying **extremely quickly**. Treat as urgent **suspected functional defect**: instrument actual damage-per-second and wound count and verify no doubled wound events/ticks, stacking from a single wound or timer inaccuracies. **Existing approved 3 HP/s per severe wound remains until explicitly changed**; if data show compliant yet overly harsh balance, report with measured survival time and options for user decision rather than lowering it silently.
- **World management:** **remove Archive World functionality entirely**. World selection instead uses a clear **Select World** button opening a **modal/list panel** of all saved worlds, with details about each world's survivor (name, status/progression as genuinely known; plus useful grounded world details). Select/open from this panel. **Delete World** action lives inside the same world-selection panel, with exact-name confirmation and recoverable trash/backup where feasible. Not a dropdown menu; preserve general no-dropdown preference.
- **TP passives:** audit existing costs/effects/implementation and present proposed rebalancing for approval; do not silently change them.
- **Animal harvest:** harvesting knife only; no tool bypass.
- **Auto-gather:** smarter paths and opt-in/out options per eligible resource, previous ground>carcass>tree/boulder and 60s drop exclusion still apply.

**Implementation verification:** use exact approved resource list above plus full user-approved equipment/food/medical rules as authority; produce an explicit kept/removed item table so the user can inspect whitelist enforcement. Old saved worlds can be incompatible without rollback migration. Do not start Codex until user authorizes another instruction.

## Approved Select World screen concept — 2026-11-23

- User explicitly approved the **Select World panel concept** shown in chat for the next Project Ragnarok Codex build.
- Main menu has **Select World** button. Clicking opens a proper panel/modal with **all available saved worlds**, each showing the **world name, survivor name and meaningful survivor details** such as progress/level/status where available, plus useful world metadata.
- The panel offers an obvious **selection indicator** and controls for **entering/continuing selected world** and **deleting selected world**. Show actual saved-world data, not the sample mockup names ("Northern Shores", "The Last Settlement").
- **World deletion** requires clear named confirmation; prefer recoverable backup/trash rather than immediate irreversible removal. Do not allow accidental deletion of the active world or another user's world.
- **Remove Archive World** functionality entirely; do not replace this panel with a dropdown. The UI should fit the game's established aesthetic, scale and control scheme.
- This is approved for **next authorized Codex build**, not yet implemented. No local game changes or public website updates from recording the decision.

## v0.18.0 solo playtest — usability, NPC systems and critical successor bug (2026-11-23 night)

**Source:** User's live solo feedback with two screenshots (inventory/storage and shoreline with follower Einar). **Status:** user-requested fixes/features to include in a subsequent authorized Codex pass; not implemented, no success claims. Compare to ongoing current code before coding and preserve source backups. Original screenshots in chat are visual context, not local GitHub files.

### Critical progression blocker — fix first
- After survivor death, successor creator **cannot confirm**. Error reported exactly: **"could not write the checkpoint. Your TP is unchanged."** Reproduces whether TP points are spent or not. Trace checkpoint write/validation, survivor succession, saved equipment, grave inventory and profile/world paths; produce actionable failure diagnostics and tests for both TP conditions. Do **not** treat as TP point accounting alone. Fix checkpoint atomicity; never lose inventory, TP or world state. Try actual native end-to-end death→successor creation→save/reload.

### Inventory, storage and crafting UI
- **Inventory-screen hotbar** remains too large and still contains a scrollbar. Shrink to fit its allocated width (previous explicit 15% reduction) and eliminate scrollbar; show slot item quantities in bottom-right consistently, without resizing normal gameplay HUD hotbar.
- **Crafting categories should be visible tabs**, not previous/next arrow selectors or dropdowns. Keep category navigation clear and fit available width.
- Recipe button should contain compact ingredient quantities and their **inline icons**, e.g. `5 × [approved resource icon], 3 × [approved resource icon]`; remove redundant separate icon row below recipe button. Maintain legibility, full ingredient and tool information and responsive UI without horizontal overflow.
- Add an approved **Mortar & Pestle crafting recipe**, but its **ingredients and required tools/station have NOT been specified by the user**. Do not invent those as if approved; present a concise proposed recipe for approval (or leave the acquisition path functional while awaiting it).
- Chest resource artwork currently renders **abnormally large** and obscures the fixed slots; apply same controlled icon sizing as backpack. **Show stack quantities at bottom-right of each slot**.
- Chest should have a **fixed grid layout/dimensions independent of how many items are present** (within chest's actual capacity), rather than dynamically expanding/collapsing with contents.
- Add **Nearby Stack to Chests** action from inventory button and/or hotkey to deposit matching compatible player items into reachable chests without duplication, with clear range/ownership and safe multiplayer authority.
- **Ctrl + left-click** quick-transfers selected item / entire stack between appropriate open inventories and containers; preserve hotbar references, eligibility, capacity and stack counts.

### Gathering, combat and navigation
- During held auto-gather, **retain a drawn dedicated axe/pickaxe/knife across consecutive same-tool actions**, only stowing/switching if next target requires another tool or the held auto-gather key (Space in current controls) is released. Then restore precisely the prior equipped weapon/item state. Do not stow axe between each tree swing.
- **Auto-gather should collect dropped/recoverable arrows** when eligible, with the existing individual 60-second protection for player-dropped items, corpse/grave exclusions and inventory checks. Arrow recovery is not interchangeable with user-dropped item cooldown.
- **Auto-gather pathing still struggles around obstacles.** Improve actual navigation and stuck recovery through rocks, trees, POI geometry and shore; skip unreachable targets rather than spin or run into collisions.
- **Boulder mining/harvesting still not functioning** in the user's live build (shoreline screenshot). Instrument interaction target detection, dedicated pickaxe gating, auto-gather/manual path, valid boulder types and depletion; fix for real world placed boulders without introducing forbidden generic `stone` drops.
- **Ranged uphill shots still fail**. Crosshair is authoritative intentional aim point: aim-assist/trajectory solve from projectile origin to crosshair world target when physically reachable, with appropriate projectile ballistics, without punishing camera elevation. Do not mislead with target outlines; genuinely hit when shot is valid. Test several steep slopes at real native frame rates.
- **Enemy outline should be a single basic red exterior silhouette**, not assorted internal body-part outlines. Use mesh grouping/depth-aware outline appropriate to final visible target; no red interior artifacts and no highlighting obstructed targets.
- On map and minimap, player marker must be **directional arrow rotating to actual survivor facing**.

### Water and creature interaction
- Swimming currently moves but **character should sink until waterline is at least 3/4 up the torso** while swimming, with sensible buoyancy.
- **Suppress footsteps while swimming**; use appropriate water motion/audio instead where implemented.
- Preserve hard plague rule: infected **cannot swim**, sink and thrash. Apply water physics to NPCs and animals appropriately.

### Character appearance, NPC interaction, trophies
- In Character screen, **allow rotation of avatar model** so player can inspect trophies of valour from all angles.
- NPC interaction should offer **Inspect Health** with useful condition/wound display and allow proper treatment of selected injuries using the same approved medical supplies and rules as survivors, with authority/persistence and no free arbitrary cures.
- **Raven trophy of valour:** wings on back, intentionally **exaggerated angel-like wing size**, awarded through approved raven trophy progression.
- **Trophies of Valour upgrade visually and/or effects as player kills more of the corresponding creature/infected type**; determine milestone thresholds/effects with user or document proposals, avoid silently inventing new combat power systems.
- Four NPC aggression/engagement stances:
  - **Offensive:** attack any enemy within permitted engagement range but **do not chase beyond defined leash distance** of guarding post or current follow target.
  - **Defensive:** protect post/follow target when an aggressive enemy approaches too closely.
  - **Neutral:** only attack when NPC itself or assigned follow target is attacked.
  - **Passive:** avoid fighting, keep distance from aggressors and temporarily flee when attacked.
  Stances must operate while guarding or following and respect current plague infected senses/settlement boundaries.
- NPCs should autonomously **eat, drink and medically treat themselves** using legitimate supplies and survival rules while in village or following. No free conjured supplies. Avoid inappropriate food/medical use during active attacks.
- When player dies, **NPC followers automatically return to their home village**. Persist their status and avoid standing indefinitely at the corpse/site; do not teleport unless necessary to recover stuck pathing.

### Corpse handling and plague safety
- Add options to **decapitate dead bodies using the approved dedicated axe**, **burn remains with a torch**, or **tie tog around ankles to drag corpse** to another location, rather than picking up the potentially infectious body. The intent is to avoid fluid/contact transfer.
- Respect established plague rules: brain destruction/decapitation and burning suppress reanimation appropriately, infected animal/survivor handling, potential contagion during unsafe corpse interactions. Must not enable abuse that skips unique Fallen Champion sequence or allows auto-looting memorial bodies; discuss/implement safeguards for notable corpses separately.
- No new rope item or extra tool invented without explicit approval; user specifically cites **tog** for tying/dragging. Dragging needs basic grounded body physics, safe controls, save considerations and no unrealistic automatic disinfection.

### Build/application presentation
- Add a custom **Project Ragnarok icon to the exported Windows executable**, including Windows taskbar and window icon as appropriate; prefer existing approved branding asset or user-controlled design rather than borrowing unrelated artwork.

### QA priorities / guardrails
- First resolve **successor checkpoint failure**; next verify boulder harvesting and uphill projectile aiming in real Windows gameplay, then inventory/crafting usability and animal/NPC handling.
- Validate screenshot-reported inventory art/chest grid bugs at real UI resolution. Add multiplayer fixtures but do not equate localhost tests with physical two-PC verification.
- Current v0.18.0 updater and 11 approved original resource icons must remain intact. Avoid overwriting user's `G:\Project Ragnarok\Design Assets\Icon Art` originals or live public releases.
- Maintain user-approved resource/item whitelist, no invented resources or player weapon/tool types. Previously approved hide carrying pouches still deferred.
- Numeric proposals (mortar recipe, trophy thresholds, stance ranges, target hit compensation) should be explicitly called technical defaults/proposals, not silently misrepresented as user-approved values.

## Maintenance protocol

1. When the user approves a new design decision, add it to this register under the relevant **Approved** section.
2. Keep **Proposed / needs discussion** ideas separately and do not silently upgrade them to approved.
3. Record what Codex says was implemented separately from what has been verified through actual playtesting.
4. On official user-approved release, write structured **Added / Changed / Fixed / Known Issues** GitHub Release notes. The website Dev Log will display them automatically.
5. Preserve approved artwork as separate files with accurate names and licence provenance; avoid overwriting the reference sheet or reinterpreting it as a game-ready asset.
6. The live site notes are a curated digest of this file, not a substitute for the full decision history.

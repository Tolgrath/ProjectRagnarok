# Project Ragnarok — Next Build: Approved Crafting, Equipment & Medical Systems

**Decision date:** 2026-11-23  
**Status:** User-approved gameplay specification, **not implemented**. Include in the **next authorized Godot build**, alongside outstanding stability work, without claiming code exists yet. User has abandoned the separate 2D lab; it is out of scope. **Never add weapons or tools independently**; only those explicitly named by the user are authorized.

## 1. Resource tiers, spawn and stacks

| Tier | Item | Max stack | Source |
|---|---|---:|---|
| 1 | Stick | 100 | Randomly on ground; also berry-bush harvesting; more common near clusters of trees |
| 1 | Pebble | 100 | Random ground; somewhat more likely near rocks |
| 1 | Plant fibre | 100 | Random ground, especially from bushes and trees |
| 1 | Bark | 100 | Tree harvesting; occasionally ground near trees |
| 1 | Leek | 100 | Random ground forage, more likely near water |
| 1 | Mushrooms | 100 | Random ground forage |
| 1 | Bones | 100 | Animal harvesting; occasionally ground, more common near predators |
| 2 | Branch | 50 | Ground near trees, cutting bushes |
| 2 | Cobble | 50 | Ground, rarer than pebbles, most likely near boulders |
| 3 | Log | 25 | Cutting down trees |
| 3 | Stone slab | 25 | Mining boulders |

**Do not conflate** the previous old registry item `wood` or `stone` with the new wood/stone resource tier system. Migrate crafting, loot, inventory, storage, UI icons and legacy saves carefully; create explicit compatibility mapping without deleting user inventories or worlds. Keep user-approved resource quantities.

## 2. Breakdown requirements (exact)

| Conversion | Tool requirements | Location |
|---|---|---|
| 1 branch → 4 sticks | Stone chisel or eligible higher upgrade | On person |
| 1 cobble → 4 pebbles | Chisel + wood hammer, or eligible upgrades | On person |
| 1 log → 4 branches | Chisel + hammer, or eligible upgrades | Workbench |
| 1 log → 16 sticks | Chisel + hammer, or eligible upgrades | Workbench |
| 1 stone slab → 4 cobbles | Chisel + hammer, or eligible upgrades | Workbench |
| 1 stone slab → 16 pebbles | Chisel + hammer, or eligible upgrades | Workbench |

**Every workbench resource breakdown requires BOTH chisel and hammer**, even if earlier instructions mentioned only chisel. No resource/output multiplication beyond given yields.

## 3. Crafted material, equipment and ammunition

All tool prerequisite checks use the equipped permanent tool slot, not consumable inventory items.

| Item | Exact crafting recipe | Tool / station | Max stack |
|---|---|---|---:|
| Tog | 2 plant fibre | not specified; do not invent station requirement | 50 |
| Stone chisel | 2 cobble | no prerequisite specified | permanent dedicated chisel tool slot |
| Stone axe | 1 stick + 1 cobble + 1 tog | chisel or higher | permanent axe slot |
| Stone pickaxe | 1 stick + 2 cobble + 1 tog | chisel or higher | permanent pickaxe slot |
| Wood hammer | 2 sticks + 1 tog | chisel or higher | permanent hammer slot |
| Wood hoe | 1 stick + 1 branch + 1 tog | chisel or higher | permanent hoe slot |
| Wood shovel | 2 sticks + 1 branch + 1 tog | chisel or higher | permanent shovel slot |
| Stone knife | 1 stick + 1 cobble + 1 tog | prerequisite not specified | permanent knife slot |
| Stone sword | 1 stick + 2 stone slabs + 1 tog | chisel or higher | 1 |
| Stone battle axe | 1 stick + 2 cobbles + 1 tog | chisel or higher | 1 |
| Wood spear | 1 branch + 2 tog | chisel or higher | 1 |
| Sling | 1 stick + 1 tog | **no tool required** | 1 |
| Wood bow | 1 branch + 1 tog | no tool prerequisite specified | 1 |
| Throwing javelin | 1 branch + 1 tog | chisel or higher | 10 |
| Wood arrows | 1 stick → 1 / 1 branch → 4 / 1 log → 16 | chisel or higher | 100 |
| Pebbles for sling | 1 cobble → 4 / 1 slab → 16 | chisel + hammer; on person for cobble, workbench for slab | 100 |

**Javelins are recoverable after throwing.** Wood arrows are recoverable after impact, but **15% chance of breaking on enemy contact**; no assumption that world/terrain hits have the same probability. Slings use pebbles; bows use wooden arrows or higher approved ammunition. Other already-discussed combat ideas or historical suggestions are NOT permission to add an item without the user explicitly including it.

## 4. Dedicated permanent tools (important global rules)

- One **permanent named slot** for each approved tool: axe, pickaxe, shovel, hoe, building hammer, chisel, harvesting knife. Tools occupy **no backpack or hotbar slots**. No spare tool copies in backpack or chest. Each category has one persistent tool.
- Tools are **non-combat**: cannot be used as emergency weapons. Dedicated weapons serve all combat roles.
- When interacting with a relevant resource/action, the game checks the appropriate tool slot and automatically draws that tool for the animation/action, then returns it to its slot; no manual hotbar juggling.
- Tool upgrades modify the *same tool in the same slot*, without creating, replacing, transferring or destroying a second tool. Exact future upgrade stages/materials are **not approved**. Do not invent stone→bronze→iron progression as an implemented feature.
- No tool durability, wear, repair loop or consumption during crafting. Tool requirements are eligibility checks only.
- If a slot has not yet been acquired/crafted, it is unavailable until acquired by the established crafting process. Ensure starting state cannot bypass prerequisites; stone chisel has no tool prerequisite.
- No additional weapons or tools without explicit user authorization. The newly named medical tools (bone saw, mortar & pestle) are **explicit exceptions** authorized by the user. How they map to dedicated slots versus medical equipment can be implemented consistently, without inventing other tools.

## 5. Physical wounds and bleeding: latest correction is authoritative

**Each individual wound causes at most ONE bleeding subtype (normal or severe), never both.** A survivor with multiple separate wounds **can** have different bleeds active simultaneously. Keep bleeding state linked to the wound that caused it.

| Wound | Cause | Chance normal bleed | Chance severe bleed | Treatment |
|---|---|---:|---:|---|
| Scratch | Attacks or bites | 50% | 0% | Basic wrap |
| Deep scratch | Attacks or bites | 50% | 50% | Stitch kit + basic wrap |
| Bite | Bite attacks | 75% | 25% | Disinfectant paste + basic wrap |
| Infected scratch | Infected Viking/animal attack, user-specified 5% infected-wound chance | apply subtype suitable to underlying scratch; preserve single type/wound | — | Disinfectant paste + basic wrap |
| Infected deep scratch | Infected Viking/animal attack, 7.5% infected-wound chance | underlying deep-scratch bleed rules; **never double-roll to add both** | — | Disinfectant paste + stitch kit + basic wrap |
| Infected bite | Infected Viking/animal bite, 10% infected-wound chance | underlying bite bleed rules; **never double-roll to add both** | — | Water wash + disinfectant paste + basic wrap |

- **Normal bleeding:** **−2 HP/second** until the associated wound receives treatment.
- **Severe bleeding:** **−3 HP/second** until the associated wound receives treatment.
- **Do not combine 2+3 for the SAME wound**; user explicitly rejected 5 HP/s on one wound. Multiple independent bleeding wounds damage independently.
- **Temporary severe-bleed patch:** a basic wrap alone suppresses severe-bleed damage **for 60 seconds**, but **does NOT heal the wound**. Then the wrap falls off and **the original −3 HP/s severe bleed resumes** if the underlying wound has not received proper treatment. If proper treatment occurs during the minute, there is no resumption.
- The previously mentioned **20-second scratch duration was a typo**; **do not implement** it as a scratch timer or a bleed timer. The user replaced bleeding durations with until wound treatment.
- Infected scratch/deep scratch/bite cause visible wound discolouration on the character.

**Important ambiguity to be surfaced in implementation notes rather than invented:** how secondary injury roll probabilities precisely combine with the chance that a specific attack creates a wound, and how bleeding subtype is chosen on infected wound variants if existing 3D code has different mechanics. Preserve user's unambiguous percentages, and avoid inventing new probabilities or ordinary infection systems.

## 6. Plague infection — no ordinary wound infection system

- **All infected wound types refer to the zombie plague**, not an unrelated bacterial/ordinary infection. **Do not add an ordinary wound infection mechanic.**
- **Plague infection progression (newer values supersede prior 0–35 etc):**
  - Lesser **0–40%**: ideal treatment leek soup.
  - Greater **41–60%**: ideal herbal remedy; leek soup less effective.
  - Severe **61–85%**: ideal amputation of infected limb using bone saw + stitch kit; herbal remedy less effective, leek soup ineffective; **cannot amputate head or torso**.
  - Critical **86–100%**: no cure; death.
- Preserve other established plague rules: bodily-fluid transmission, progression/incubation/reanimation, dead-host viability ~24h, infected senses and behaviour, animal susceptibility and potential treatment where appropriate.
- Ailments like high fever/weakness should not be invented as universal effects; investigate triggers in existing implementation separately.
- The user explicitly intends visible discolouration of plague-infected wounds.

## 7. Food poisoning

- Caused by raw meat or poisonous vegetation consumption.
- Mushroom soup is the treatment.
- Untreated duration: **300 seconds**.
- During poisoning, **hunger and thirst drain 10% faster than their actual base rates** (multiply each existing base depletion rate by **1.10**).
- **Codex must inspect the actual base hunger and thirst rates in the Godot source and report them before/when applying this multiplier.** Do not invent them or replace existing global survival balance.

## 8. Medical and crafted items

| Item | Exact recipe | Tool / station | Max stack |
|---|---|---|---:|
| Basic wrap | 4 plant fibre | On person | 10 |
| Needles ×5 | 1 bone | Hammer; on person | 200 |
| Thread | 2 plant fibre | Knife; on person | 200 |
| Stitch kit | **1 needle + 2 thread + 1 bark** | On person | 10 |
| Disinfectant paste | 2 leek + 1 water | On person | 10 |
| Leek soup | 4 leek + 1 water | Campfire | not specified |
| Mushroom soup | 4 mushrooms + 1 water | Campfire | not specified |
| Herbal remedy | 4 leek | Mortar & pestle; on person | not specified |
| Bone saw | 1 bone + 1 stick + 2 tog | Chisel; on person | not specified |

- The stitch kit previously had four thread; this was **explicitly replaced by TWO**.
- Water wash is required for infected bites. Use existing water correctly; do not invent unrelated first-aid materials.
- User approved **bone saw** and **mortar & pestle** by name. No other medical tools may be added without explicit instruction.
- No extra recipe ingredients, item types, tool wear or crafting-tool consumption.
- Retain exact stack maxima where provided; for unspecified stack sizes, record the question and choose compatibility-safe handling rather than claiming a user-approved value.

## 9. Integration and regression requirements

- These approvals are for the **NEXT authorized 3D build** and should integrate with current multiplayer stability priorities rather than overwrite v0.16 local candidate blindly.
- First back up the whole local project and world saves. Preserve old items via versioned migration/aliases; report every changed/removed old item or recipe and avoid deleting existing player possessions.
- Update world spawns, tree/boulder/bush harvest tables, tool slots, item inventory/storage, crafting at field/workbench/campfire, equipped tool auto-selection, resource processing and UI.
- Medical treatment and bleeding/plague status must be per-survivor and per-wound, persisted through saves and synchronized host/guest without duplicated damage or item consumption.
- Add deterministic tests for every recipe, per-wound exclusive bleeding, multiple wounds, one-minute temporary severe patch, infection-stage boundaries, treatment gating, stack limits, weapon ammo and recoverability, direct-tool upgrade identity, and both co-op clients.
- **Full physical two-PC testing is pending.** Do not claim a local loopback test proves real LAN success.
- Do NOT begin coding simply because the design specification was recorded; the user must authorize Codex implementation. Do not publish the build or change the website until the user approves a release.

## 10. Remaining open questions, not license to invent

- The stone knife crafting prerequisite, wood bow crafting-tool prerequisite and tog station/tool requirement were not specified.
- The precise acquisition/create flow for permanent tool slots and medical tools must be implemented consistently without inventing extra gear.
- Natural duration for non-bleeding deep scratches/bites, if any; do not assume previous typo of 20 seconds.
- Tool upgrade material tiers and recipes are not approved.
- Soup, herbal remedy, bone saw and mortar/pestle stack limits are not yet approved.
- Confirm final behaviour of plague exposure chances versus the wound-event rolls; percentages must not be silently compounded or double-counted.

**Authority hierarchy:** most recent direct user correction > older approved design notes > Codex observations; proposed assistant ideas are not approvals.

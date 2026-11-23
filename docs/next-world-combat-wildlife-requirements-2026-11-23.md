# Project Ragnarok — World, Camera, Wildlife, Combat and Control Requirements
**Recorded:** 2026-11-23. **Status:** User-requested design direction for an upcoming build; not confirmed implemented. Do not publish or modify the Godot project from this documentation action.

## Approved/requested now
1. **Island map:** World must be an island with sea around it. Increase current map size by **50%** and include **at least one river**. The v0.16 implementation audit reported a seeded map of 160×160 metres, legacy 100×100 metres. **Important unresolved interpretation:** 50% increase to side lengths would be 240×240 m (125% increase in surface area), whereas 50% increase in area would be approximately 196×196 m. Do not silently finalize this ambiguity; confirm when preparing technical implementation. Preserve saved worlds, procedural seed consistency, POI discovery and performance.
2. **Wildlife:** Ravens, rabbits, deer, wolves, boars and bears. Deer/wolves/boars/bears are reportedly already present; ravens and rabbits are requested additions. Keep sensible biology and performance-conscious AI, no unrequested fantasy creatures.
3. **Enemies:** At least **two class-based reanimated survivor variants** and reanimated animals, consistent with existing plague and infected behaviour rules. Base roles/classes should be selected from actual implemented class definitions; do not invent new classes.
4. **Camera freedom:** Current pitch restrictions are too limiting. Allow more freedom to look higher and lower with responsive camera and functional obstacle handling.
5. **Combat stance/aiming:** While holding **RMB** to lock character facing, show a visually pleasant crosshair for **both melee and ranged**. Hide when released. Ranged weapon aiming must not be incorrectly coupled to camera angle; test accurate projectiles across camera pitches/terrain. Existing bug: shots hit ground immediately in front of character.
6. **Auto-gather:** Include tree cutting and boulder harvesting using automatically selected eligible permanent dedicated tools; respect depletion, reach, inventory and host authority.
7. **Keybinding settings:** Provide more customizable game keybind options; handle conflicting bindings, defaults, save/load.
8. **Crouch/sneak:** Add crouching so survivors can sneak around infected. Detection must respect existing sight, sound and smell rules. Exact input and numerical stealth factors not yet user-specified.
9. **Procession of the Fallen:** Get the previously approved death/funeral procession working **in single-player** (not dependent on a co-op session). Preserve persistent death, memories/memorials and recoverable physical belongings.

## Explicitly future, NOT for immediate implementation
- The Forest-style **animal-hide pouches** to increase capacity for *specific types of items*. User wishes to investigate this later. No pouch types, recipes, sizes, material requirements or upgrade system have been approved.

## Cross-cutting boundaries
- The user's separately locked tool/weapon roster remains locked; **do not add any weapons or tools without explicit user authorization**.
- Existing v0.17 candidate is **local, Codex-reported tested, not publicly approved**. Next user playtests primarily solo; co-op roughly every other weekend. Solo passing does not verify co-op.
- Do not lose saved worlds or regress network code to implement larger terrain or new AI. Keep versioned backups and measured performance.
- The existing full design decision register and 2026-11-23 crafting/medical specification remain authoritative. Never interpret assistant-suggested detail as user-approved numeric rules.

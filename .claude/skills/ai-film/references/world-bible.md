# Phase 1 — World Bible

Goal: give the AI enough about the space that the camera can go *deeper* than a backdrop.
The world must make the character's colors pop and give every scene a reason to exist.

Formula: **Place + Era + Spatial structure + Materials + Lighting + Atmosphere + Props/Tools**

## The 7 slots

| # | Slot | Answer these | Example (Lost Temple) |
|---|---|---|---|
| 01 | Place & era | Country/region, period (ancient/modern/future), cultural roots, the backstory of the place | Abandoned jungle step-pyramid, ancient Maya-inspired, sealed for 1,000 years |
| 02 | Spatial structure | Entrance → main space → exit; layers (enter → explore → go deeper → escape); key levels | Overgrown gate → trap corridor → idol sanctum → collapsing exit tunnel |
| 03 | Materials | Surfaces, stone/metal/wood/cloth/water, wear (oxidized, cracked, moss), reflectance (gloss, warmth, glare) | Carved sandstone, gold idol, moss, roots through cracks, dust on every ledge |
| 04 | Lighting system | Source (natural/artificial), color temperature (cold/warm/neutral/vivid), time of day, how light makes depth | Torchlight inside (warm 2000K), god-rays through cracks, cool daylight outside |
| 05 | Atmosphere | Weather, dust/smoke/fog, humidity, ambient sound, risk (sandstorm, pressure) | Thick dust motes, humid haze, distant dripping, low rumble |
| 06 | Props & mechanisms | Key objects, interactable items (traps, tools, keys), how they're used or destroyed | Gold idol on pressure plate, rotating stone disc, spike wall, falling blocks |
| 07 | Story function | Per space: before (emotion/setup), during (action/decision), after (result/consequence) | Sanctum = the turn: taking the idol triggers collapse |

## Questions to ask the user (only the ones the script doesn't answer)

- Where and when is this? Real place, inspired-by, or invented?
- What does the space *feel* like in one word? (claustrophobic, sacred, rotting, sterile…)
- What's the single most memorable object in this world?
- Is there a light change during the film? (torch dies, dawn breaks, alarm red) — light changes are free drama.

## Output format (paste into FILM.md)

```
WORLD LINE (verbatim in every prompt):
<one sentence: place, era, materials, light, atmosphere>

LOCATIONS
L1 <name> — <what it is> — light: <state> — palette: #xxxxxx #xxxxxx #xxxxxx
L2 ...

LIGHTING STATES
<name>: <source, temperature, direction, mood>

PROPS
<prop>: <material, size, what it does, who touches it>

PALETTE (6-10 HEX)
#1F2B17 deep jungle · #C3A64A temple gold · #C2611A torch ember · #7E6D5E dust stone · ...
```

Checklist before locking: ☐ space is clear ☐ materials are specific ☐ light is designed
(not "nice lighting") ☐ atmosphere is strong ☐ props are usable in a shot.

# Phase 2 — Character Bible

Goal: the character is so clearly defined the AI can reproduce them in every frame.
Analogy: you're writing a casting + wardrobe sheet for a stand-in actor who has never
met the real one. Anything you don't write down, they'll improvise — differently each time.

## The 7 slots

| # | Slot | Content |
|---|---|---|
| 01 | Identity | Name, age, gender, profession, role in the world |
| 02 | Signature features | Face shape, hairstyle, skin tone, build, ONE identifying mark (scar, freckles, braid) |
| 03 | Wardrobe system | Head-to-toe: top → layers → bottom → belt → shoes → jewelry → bag. Color + material + cut + one detail each |
| 04 | Props system | Everyday items, weapon/tool, special item. Where each is carried on the body |
| 05 | Expressions & body language | Default expression, 4 key emotions for this film, posture, how they move |
| 06 | Reference views | Front, 3/4, side, back, close-up face (this becomes the character sheet) |
| 07 | Continuity rules | What changes across the film (dirt, sweat, torn sleeve, wound, lost item) and at which shot |

Mark the character as ADULT with mature facial structure when they are an adult —
image models drift toward babyface otherwise.

## The Character Line (the most important 60 words in the project)

Formula:
```
<age> <gender> <role>, <build/height>, <face: shape + one feature>, <hair: color + style>,
<skin>, wearing <top>, <bottom>, <belt/gear>, <shoes>, <one accessory>
```

Example:
> 23-year-old female explorer, 168cm athletic build, sharp angular face with a small scar
> on the left eyebrow, platinum-blonde hair in two high space-buns with loose bangs,
> sun-tanned skin, wearing a black cropped tank top, olive khaki cargo shorts, brown leather
> tactical belt with pouches and cross-chest harness, tall brown lace-up combat boots,
> small bronze pendant necklace.

Rules: no adjectives without nouns ("cool outfit" ✗). Same order every time. Never
paraphrase it later — copy-paste.

## Personality line (for acting direction, not appearance)

`Personality: <3 traits>. Moves: <how>. Under pressure: <behavior>.`
> Personality: calm, decisive, observant. Moves: low and economical, like a climber.
> Under pressure: goes quiet and fast, never screams.

## Continuity table

| State | From shot | Change |
|---|---|---|
| Clean | 1 | — |
| Dusty | 6 | dust on arms and shorts |
| Cut | 11 | thin scratch on right cheek |
| Idol in hand | 9 | carries gold idol in left hand to end |

Every keyframe prompt for that shot appends the current state.

## Checklist before locking

☐ face approved on a generated sheet ☐ wardrobe head-to-toe ☐ props placed on body
☐ 4 emotions defined ☐ continuity table done.

# Phase 4 — Master Prompt (the three-layer sentence structure)

Goal: one shooting document that the model can read like a spec. Clear structure, complete
info, precise, easy to understand.

Three layers of information in every generation:
1. **Global** — rules for the whole film (what never changes)
2. **Subject** — Character Line + current continuity state
3. **Shot** — size / lens / move / action / sound for this one shot

## Global zone template

```
FORMAT: <length>s / <BPM> BPM / <N> SHOTS / <genre feel>, cuts on the beat, shots <x>-<y>s, total <length>s, <aspect>.
THEME: Image 1 = character sheet (identity), Image 2 = world plate (location), Image 3 = <extra ref>.
SETTING: <World Line>.
MOOD: <3 words — e.g. mysterious, tense, pursuit>.
MUSIC: <instrumentation + rhythm — e.g. low sub hits + electronic pulse + heavy drums, builds to drop at 0:10>.
STYLE: <hyper-real / cinematic realism / anime / 3D>, <grade — e.g. teal shadows, amber highlights, crushed blacks>, <film texture — e.g. 35mm grain, anamorphic flares>.
LOGIC RULES: Keep the character identical in every shot (face, hair, outfit, props). Keep lens family, color grade and time-of-day consistent. Camera moves stay motivated. Fast rhythm, three-act structure, climax at <t>s.
```

## Shot zone template

```
SHOT 1 (0.0–1.5s): WS, 35mm, slow push-in / <subject + one action> / SFX: <2 sounds>
SHOT 2 (1.5–3.0s): ECU, 85mm, static / ... / SFX: ...
...
SHOT 14 (DIALOGUE BEAT, 1.5s): ECU, 85mm / <who> says: "<line>" / SFX: ...
```

## Deriving the per-shot generation prompts

Each shot becomes TWO prompts on Higgsfield.

**A. Keyframe prompt (image)** — the frozen frame at the peak:
```
<shot size> <angle> shot, <lens>mm lens, <Character Line>, <continuity state>,
<pose/action at the peak moment>, <expression>, in <location from World Bible>,
<lighting state>, <atmosphere>, <STYLE line>, <aspect> frame, no text, no watermark
```

**B. Motion prompt (video)** — what happens over time. Keep it short; the image already
carries the look:
```
<camera move> — <subject does ONE action>, <secondary motion: dust, hair, torch flicker>,
<speed: slow / sudden / continuous>. <genre> cinematic, consistent character.
```
Motion prompt rules: one subject action + one camera move. Describe physics
("dust bursts from the floor as her boot lands") not feelings ("she feels determined").

## Common errors

- Writing appearance only, no style ➜ looks generic.
- Writing style only, no character content ➜ face drifts.
- No single logic rule ➜ every shot has a different grade/lens/time of day.

## Final output check

☐ structure is clear ☐ info is complete ☐ rules are clear ☐ every shot is shootable with one camera

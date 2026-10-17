---
name: ai-film
description: >-
  Turn a film idea or script into a finished 15-60s AI cinematic short on Higgsfield.
  Builds four locked layers in order — World Bible, Character Bible, Shot Breakdown,
  Master Prompt — then generates character sheets, world plates, per-shot keyframes and
  per-shot video clips, and cuts them to a BPM grid. Use when the user says "make a film",
  "AI film", "short film", "trailer", "teaser", "cinematic short", "storyboard my script",
  "shot list", "turn my script into shots", "/ai-film", or brings a script, logline or
  story idea and wants AI-generated cinematic video.
---

# AI Film: script → world → character → shots → master prompt → film

**Core idea: see the world first, then look through the lens.**
Think of a film studio. The production designer builds the set (World), then wardrobe
dresses the actor (Character), then the director plans every camera setup (Shots), then
the script supervisor writes one shooting document everyone obeys (Master Prompt).
The AI is the crew. It only works as well as the brief it gets.

Every layer is **locked** before the next one starts. A detail defined once is reused
word-for-word in every later prompt — that is what keeps the film consistent.

All work for one film lives in one workbook: `films/<slug>/FILM.md`, copied from
`templates/FILM.md`. Generated assets go next to it in `films/<slug>/assets/`.

---

## Phase 0 — Brief (one interview, then confirm)

Ask in ONE message. Skip anything the user already gave.

| Must have | Default if user says "you decide" |
|---|---|
| Logline / script (1-3 sentences minimum) | — required |
| Length | 15s |
| Aspect ratio | 16:9 (9:16 for Reels/TikTok/Shorts) |
| Genre + mood | from the script |
| Visual style | hyper-real cinematic |
| Music tempo (BPM) | 120 for drama, 160 for action, 90 for emotional |
| Dialogue? Which lines? | none, or one line at the climax |
| Budget ceiling (credits) | ask — never assume |

Then write back a 5-line **Brief Card** (title, logline, length/aspect/BPM, style,
emotional arc) and get a "yes" before Phase 1.

Challenge the brief: if the story has no turn (no moment where something changes),
say so and propose one. A 15s film still needs: setup → turn → payoff.

## Phase 1 — World Bible   → `references/world-bible.md`

Fill the 7 world slots: **Place & era · Spatial structure · Materials · Lighting system ·
Atmosphere · Props & mechanisms · Story function of each space.**
Output a locked **World Line** (one sentence reused in every prompt) plus 2-4 named
locations, each with its own lighting state and HEX palette.

## Phase 2 — Character Bible   → `references/character-bible.md`

Fill the 7 character slots: **Identity · Signature features · Wardrobe system ·
Props system · Expressions & body language · Reference views · Continuity rules.**
Output a locked **Character Line** (≤60 words, reused verbatim in every shot that shows
them) and a continuity table (what changes over the film: dirt, wounds, lost props).

Original characters only. If the user names a celebrity or existing IP, use it as a loose
vibe and build a distinct original person.

## Phase 3 — Shot Breakdown   → `references/shot-breakdown.md`

1. Story beats first (6-beat spine: Establish → Goal → Enter subject → Reaction → Action → Exit).
2. Expand beats into shots. Each shot gets a **shot key**: Info · Action · Peak.
3. Assign shot size, lens, angle, camera move, duration — snapped to the BPM grid.
4. Check transitions (match action, angle change, screen direction, pacing).
5. Run the clean-shot checklist before moving on.

Shot-count rule of thumb: `shots ≈ length_in_seconds ÷ 1.5` for action, `÷ 3` for drama.

## Phase 4 — Master Prompt   → `references/master-prompt.md`

Assemble the two-zone script:
- **Global zone**: FORMAT · THEME (refs) · SETTING · MOOD · MUSIC · STYLE · LOGIC RULES
- **Shot zone**: one line per shot — `SHOT n (t0–t1): SIZE, lens, move / action / SFX:`

Then derive the **per-shot generation prompts** (keyframe prompt + motion prompt) from it.
Show the user the full Master Prompt and get a "yes" before spending credits.

## Phase 5 — Generate on Higgsfield   → `references/higgsfield-production.md`

Order matters — each step feeds references to the next:
1. Character sheet (image) → user approves the face. **Nothing else until the face is locked.**
2. World plates (image, one per location).
3. Keyframes (image, one per shot, using character sheet + world plate as references).
4. Clips (image-to-video, one per shot, keyframe as start frame).
5. Assembly: trim each clip to its grid duration, cut to music.

**Cost gate:** before every batch, state the count × model × duration and estimated
credits, check `balance`, and wait for the user's yes. Never generate on your own.

## Phase 6 — Review & iterate

For every clip check: same face? same outfit/continuity state? correct screen direction?
motion reads in the trimmed duration? Regenerate only the failing shots — change one
variable at a time (seed, prompt wording, or model), never all three.

---

## Hard rules

1. **Lock, then reuse verbatim.** World Line and Character Line are copy-pasted, never paraphrased.
2. **Write style AND content.** Every prompt states who/what (content) and how it looks (style). Missing either is the #1 failure.
3. **One logic rule set for the whole film.** Same grade, same lens family, same time-of-day logic.
4. **Generate long, cut short.** Video models have 3-5s minimums; a 1.5s shot is a trimmed 4-5s clip. Put the peak moment in the middle of the generated clip.
5. **One action per shot.** A shot that tries to do two things fails both.
6. **The face is approved by the user before any keyframe exists.**
7. **No surprise spending.** Quote, confirm, then generate.

## Files

| File | Use |
|---|---|
| `references/world-bible.md` | Phase 1 slots, questions, output format |
| `references/character-bible.md` | Phase 2 slots, Character Line formula, continuity table |
| `references/shot-breakdown.md` | Beats, shot vocabulary, durations, BPM math, transition rules, error list |
| `references/master-prompt.md` | Global + shot zone template, per-shot prompt formulas |
| `references/higgsfield-production.md` | Tool order, model choice, cost gate, assembly |
| `templates/FILM.md` | The workbook — copy per film |
| `examples/lost-temple.md` | Complete worked example (15s / 160 BPM / 15 shots) |

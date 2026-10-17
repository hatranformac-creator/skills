# Phase 5 — Production on Higgsfield

Analogy: a relay race. The character sheet passes the baton to the world plates, the
plates pass it to the keyframes, and the keyframes pass it to the video clips. If one
runner drops the baton (a wrong face), every runner after them is wasted money.

## Step 0 — Setup (free calls)

1. `balance` — know the budget.
2. `models_explore` with `action: "get"` for each model you plan to use — read its
   durations, aspect ratios and media roles. Don't trust memory; models change.
3. Quote the full plan to the user:
   `N images × model + N clips × model × seconds ≈ X credits` → wait for "yes".

## Step 1 — Character sheet (image)

- Load `get_workflow_instructions` with `workflow: "character-sheet"` and follow its
  slot architecture. Feed it the Character Bible.
- Composition: turnaround (front / 3/4 / side / back) for full-body films, or
  split-screen (full body + face close-up). 16:9.
- `generate_image`, then `jobs_wait`, then show the result.
- **User approves the face.** Iterate here until they do — this is the cheapest place
  to fix identity.
- Save the approved image id/url in FILM.md. If reference elements are available
  (`show_reference_elements` / `manage_reference_elements`), store the character as a
  named element so later calls can reuse it.

## Step 2 — World plates (image)

- One `generate_image` per location, film aspect ratio, no characters in frame:
  `<World Line>, <location>, <lighting state>, empty, cinematic establishing frame`.
- Run them together with `generate_image_batch`, then `jobs_wait`.

## Step 3 — Keyframes (image, one per shot)

- Keyframe prompt from master-prompt.md, formula A.
- Pass the character sheet + the right world plate as reference images.
- Generate as a batch. Review all keyframes as a contact sheet (`show_generation_by_ids`)
  BEFORE any video: check face, outfit, continuity state, screen direction.
- Regenerate only the failing keyframes.

## Step 4 — Clips (image-to-video, one per shot)

Pick the model per shot type (verify current options with `models_explore`):

| Need | Model (as of this skill's writing) | Why |
|---|---|---|
| Identity-critical shots (faces, CU, dialogue) | `seedance_2_0` / `seedance_2_5` | image references + identity consistency, start/end frame |
| Fast cinematic camera, genre feel | `cinematic_studio_video_v2` | genre + speedramp + multi-shot mode |
| Multi-shot sequence in one go, motion transfer | `kling3_0` | multi-shot, audio sync |
| Not sure | `models_explore action:"recommend"` | let it rank |

- `start_image` = the shot's keyframe. Add the character sheet as `image_references`
  when the model supports it.
- Duration: generate the model's minimum that fits (usually 4-5s), even for a 1.5s shot.
  Write the motion prompt so the peak happens in the middle; you'll trim later.
- Turn native audio **off** if you'll score the film with your own music (cheaper, cleaner),
  on if you want ambient SFX baked in.
- Same model for all shots in one sequence when possible — mixing models shifts the grade.
- Batch with `generate_video_batch`, then `jobs_wait`, then show all results together.

## Step 5 — Assembly

Pick one:
- **Higgsfield:** `get_workflow_instructions` with `workflow: "video-montage"` to cut the
  clips, add the music track and trims.
- **Local:** ffmpeg trim each clip to its grid duration (`-ss <in> -t <dur>`), concat, mux the
  music. Cuts land on the beat because the durations were snapped to the BPM grid in Phase 3.
- **Music:** `generate_audio` from the MUSIC line (state BPM and length), or the user's own track.
  Lay the music first, then cut picture to it.

## Step 6 — Review

Contact sheet of the trimmed cut: one frame per shot. Check: face drift, outfit drift,
continuity table respected, screen direction, a stillness hold before the climax, last
frame holds ≥0.5s. Fix by regenerating single shots only.

## Spending rules

- Quote → confirm → generate. Every batch.
- `use_unlim: true` only if the user explicitly asks to spend free-trial generations.
- If a job fails twice with the same settings, stop and change ONE thing (prompt, seed, or model).

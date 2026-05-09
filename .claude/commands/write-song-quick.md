---
description: Write one Telugu Christian song fast with smart defaults — no questions asked. Optional one-line theme as the argument.
---

# /write-song-quick

Generate one original Telugu Christian song in Suno format using the project's `song-writer` agent with smart defaults (Worship & Praise, Contemporary, Standard length, Reflective & Devotional, Contemporary Worship band, medium tempo). Skips all questions.

**Argument (optional):** `$ARGUMENTS` — a one-line theme/topic override. Examples:
- `/write-song-quick`
- `/write-song-quick గ్రేస్ — God's grace and mercy`
- `/write-song-quick Good Friday — the cross and the blood`
- `/write-song-quick Daniel in the lions' den, narrative praise`

## Behavior

1. **Resolve theme.**
   - If `$ARGUMENTS` is empty → `THEME_OVERRIDE = ""` (agent uses default: Worship & Praise).
   - Otherwise → `THEME_OVERRIDE = $ARGUMENTS` (agent infers mood/style from it; everything else stays default).

2. **Announce the plan in 2–3 lines.** State the resolved theme + that the song will be written to `created songs/`. No further planning prose.

3. **Spawn agents in parallel** (single message, two Agent calls):
   - **`song-writer`** — pass:
     - `THEME_OVERRIDE`: the resolved theme string (or `""`)
     - `OUTPUT_DIR`: `created songs/`
     - `EXTRA_NOTES`: any extra creative direction the user included after a `—` or `,` in `$ARGUMENTS`
   - **`monitor`** — pass:
     - `RUN_ID`: `write-song-quick-<timestamp>`
     - `EXPECTED_OUTPUTS`: `["created songs/telugu_christian_song_*.txt"]` (glob — newest match counts)
     - `WORKERS`: `["song-writer"]`
     - `OUTPUT_PATH`: `.claude/agent-output/monitor/write-song-quick-<timestamp>.md`

4. **Collect.** Read the song-writer's reply for the output path. Verify the file exists with one Glob/Read.

5. **Report** one short paragraph:
   - Song path (clickable link to `created songs/...`)
   - Theme + mood + length
   - First line of the pallavi (the hook)
   - Suggestion: `/review-songs created songs/<filename>` to audit, or paste both blocks into Suno.

## Rules

- **One song per invocation.** For multiple songs, run the command multiple times (or build a `/write-song-batch` later).
- **No questions to the user.** That's the whole point of `-quick`. If the user wants the full interactive flow, point them at the `telugu-christian-song-writer` skill instead.
- **Do not promote, move, or rename the file** after song-writer writes it — `created songs/` is the final destination.
- **Do not run `git`.** No commit, push, or add — even if the run succeeds.
- **One retry max.** If the song-writer's output file is missing after the spawn returns, retry once. After that, report failure with whatever the agent said and stop.
- **Do not run the auditor or improver** as part of this command. If the user wants the full pipeline, that's a separate command (future `/write-and-review`).

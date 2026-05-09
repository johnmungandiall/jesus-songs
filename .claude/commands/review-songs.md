---
description: Audit and improve Telugu Christian songs in created songs/. Pass a glob or path to scope it; default reviews everything in created songs/.
---

# /review-songs

Run the song-quality review pipeline.

**Argument (optional):** `$ARGUMENTS` — a glob, file path, or empty.

## Behavior

1. **Resolve targets.**
   - If `$ARGUMENTS` is empty: glob `created songs/*.txt`.
   - If `$ARGUMENTS` is a directory: glob `<dir>/*.txt`.
   - If `$ARGUMENTS` is a glob (contains `*`): use it directly.
   - If `$ARGUMENTS` is a file path: use that single file.
   - If no `.txt` files match: report "no songs found" and stop.

2. **Plan and announce.** Print the list of songs to review and the agent count (one auditor per song + one monitor, capped at 4 parallel auditors per batch).

3. **Phase A — Audit (parallel).** Spawn one `song-auditor` per song, plus one `monitor`, in a single message. Pass each auditor:
   - `SONG_PATH`: absolute path to the song
   - `OUTPUT_DIR`: `.claude/agent-output/song-auditor/`
   And pass the monitor:
   - `RUN_ID`: `review-songs-<timestamp>`
   - `EXPECTED_OUTPUTS`: list of expected review file paths
   - `WORKERS`: list of auditor names spawned

4. **Collect reviews.** Read each `<song-basename>-review.md`. Parse the `Recommended Action` line.

5. **Phase B — Improve (parallel).** For every review with action "Send to song-improver", spawn one `song-improver` in parallel. Pass each:
   - `SONG_PATH`: absolute path to the original song
   - `REVIEW_PATH`: absolute path to the review markdown
   - `OUTPUT_DIR`: `.claude/agent-output/song-improver/`
   Also spawn a final `monitor` pass with the expected improved-song paths.

6. **Report.** Print a table:
   - Song | Score | Action | Improved file (if any)
   And note where to find every artifact.

## Rules

- Cap at 4 auditors in flight at once. If more songs, batch them.
- Skip Phase B entirely if no review recommended improvement.
- Do NOT promote improved files into `created songs/`. Leave them under `.claude/agent-output/song-improver/` for the user to inspect and copy over.
- Do NOT run `git` commands.
- If an auditor's output file is missing after the spawn returns, retry that one auditor once. After one retry, mark it failed and continue.

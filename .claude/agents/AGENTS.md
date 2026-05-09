# Agent Registry — jesus-songs

This project's agent team for reviewing and improving Telugu Christian songs.

## Active Agents

| Name | Role | Model | Tools |
|------|------|-------|-------|
| [song-auditor](song-auditor.md) | Scores a song on Suno format, Telugu fluency, theology, and singability. Outputs a structured review. | haiku | Read, Write, Glob, Grep |
| [song-improver](song-improver.md) | Takes a song + auditor review and rewrites only the flagged parts. Preserves theme, mood, structure. | sonnet | Read, Write, Glob |
| [monitor](monitor.md) | Watches agent-output directories during a run and reports which expected files exist. | haiku | Read, Glob, Bash |

## Pipelines

### `/review-songs` — full review pipeline
1. Glob `created songs/*.txt` (or a user-supplied path)
2. Spawn one **song-auditor** per song in parallel + one **monitor**
3. Filter reviews where `Recommended Action` is "Send to song-improver"
4. Spawn one **song-improver** per flagged song in parallel
5. Final monitor pass and report

## Output Locations

| Agent | Output |
|-------|--------|
| song-auditor | `.claude/agent-output/song-auditor/<song-basename>-review.md` |
| song-improver | `.claude/agent-output/song-improver/<song-basename>-improved.txt` and `<song-basename>-changes.md` |
| monitor | `.claude/agent-output/monitor/<run-id>.md` |

## Conventions

- Agents never run `git commit`, `git push`, or `git add`.
- Improved songs are written to `.claude/agent-output/song-improver/`. Promoting them to `created songs/` is the user's call.
- All `.txt` lyric files use the Suno tag set: `[Verse N]`, `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[End]`. No `[Intro]` or `[Outro]`.

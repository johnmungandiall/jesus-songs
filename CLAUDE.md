# jesus-songs

Telugu Christian song lyrics generated for Suno AI.

## Conventions

- All generated `.txt` lyric files go in `created songs/`. After a song is tested in Suno and accepted, the user may move it to `tested/`. Never write generated songs to the project root.
- Lyric files use Suno tags only: `[Verse N]`, `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[End]`. No `[Intro]` or `[Outro]`. No parenthetical musical directions like `(soft piano)`.
- Lyrics are written in Telugu script (తెలుగు), not transliteration.

## Agent Pipeline

A multi-agent review pipeline lives under `.claude/`. See [.claude/agents/AGENTS.md](.claude/agents/AGENTS.md).

- `/review-songs` — audits songs in `created songs/` and produces improved versions under `.claude/agent-output/song-improver/` for any song that needs work.
- Improved songs are NOT auto-promoted. The user reviews them and copies the keepers into `created songs/`.

## Git

Agents do not run `git commit`, `git push`, or `git add` unless the user explicitly asks.

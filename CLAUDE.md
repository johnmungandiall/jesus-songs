# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# jesus-songs

Telugu Christian song lyrics generated for Suno AI, plus a multi-agent pipeline that writes, audits, and improves them.

## What flows through this repo

A song's lifecycle:

1. **Generated** by either `/write-song-quick` (fast, smart defaults) or the `telugu-christian-song-writer` skill (interactive question flow). Both write a `.txt` file to `created songs/`.
2. **Tested** by the user in Suno (paste the two blocks into Suno's "Style of Music" and "Lyrics" fields).
3. **Reviewed** optionally by `/review-songs`, which audits format/Telugu/theology and produces improved versions under `.claude/agent-output/song-improver/` (never auto-promoted).
4. **Promoted** by the user moving keepers from `created songs/` into `tested/`.

## Slash commands

- **`/write-song-quick [optional theme]`** — generate one song with smart defaults (Worship & Praise / Contemporary / Standard / Reflective + Contemporary Worship band, medium tempo). No questions. Optional one-line theme override infers mood/style.
- **`/review-songs [optional path or glob]`** — audit songs in `created songs/` (or a scoped path), then improve any flagged. Two-phase parallel pipeline (auditor → improver) with a monitor.

For interactive song writing with full lyric + music questions, invoke the `telugu-christian-song-writer` skill instead of `/write-song-quick`.

## Conventions

- All generated `.txt` lyric files go in `created songs/`. After a song is tested in Suno and accepted, the user may move it to `tested/`. Never write generated songs to the project root.
- Lyric files use Suno tags only: `[Verse N]`, `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[End]`. No `[Intro]` or `[Outro]`. No parenthetical musical directions like `(soft piano)`.
- Lyrics are written in Telugu script (తెలుగు), not transliteration.
- **Songs open with `[Chorus]`, not `[Verse 1]`.** This is the Telugu pallavi-charanam tradition: the title hook is the first sung line. Every published Telugu Christian song does this.
- Output `.txt` file format is two blocks separated by a blank line:
  ```
  === SUNO STYLE PROMPT (paste into "Style of Music" field) ===
  <one English sentence: genre, vocals, "Telugu vocals", tempo, instruments, mood>

  === LYRICS (paste into "Lyrics" field) ===
  [Chorus]
  ...
  [End]
  ```

## Suno style library

`styles/` holds 100 ready-to-paste Suno "Style of Music" prompts organized into 16 folders by genre/occasion (worship-contemporary, worship-traditional, praise-gospel, indian-fusion, jazz-sophisticated, occasion-christmas, occasion-easter-good-friday, occasion-wedding, occasion-funeral, etc.). See [styles/INDEX.md](styles/INDEX.md) for the full catalog. `south indian telugu styles/` holds music-director-flavored variants (01-music-directors/, 02-song-types/).

When the user wants a style prompt without generating new lyrics, point them at `styles/INDEX.md` to browse and copy. The song-writer skill/command also generates a fresh style prompt inline.

## Agent pipeline

A multi-agent system lives under `.claude/`. See [.claude/agents/AGENTS.md](.claude/agents/AGENTS.md) for the registry and pipeline definitions. Agents:

- **song-writer** (sonnet) — writes one song using smart defaults; reads the skill's SKILL.md once for vocabulary and patterns.
- **song-auditor** (haiku) — scores Suno format, Telugu fluency, theology, and singability.
- **song-improver** (sonnet) — fixes only what the auditor flagged; preserves theme, mood, structure.
- **monitor** (haiku) — read-only run observer.

Improved songs land in `.claude/agent-output/song-improver/` and are NEVER auto-promoted to `created songs/` — the user reviews and copies keepers manually.

[WORK-SUMMARY.md](WORK-SUMMARY.md) at the project root logs every orchestration run and pipeline change.

## Git

Agents do not run `git commit`, `git push`, or `git add` unless the user explicitly asks.

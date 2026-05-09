---
name: telugu-christian-song-writer
description: Generate original Telugu Christian song lyrics formatted for Suno AI, with a matching Suno style-of-music prompt covering genre, vocals, tempo, and instruments. Use this skill whenever the user asks to create, write, or generate Telugu Christian songs, Telugu worship songs, Telugu praise songs, or Telugu devotional songs. Also trigger when users mention Suno AI format with Telugu Christian content, or ask for song lyrics about Jesus, God, salvation, worship, or praise in Telugu language.
---

# Telugu Christian Song Writer for Suno AI

Generate authentic Telugu Christian song lyrics formatted for Suno AI music generation platform, plus a tailored Suno "Style of Music" prompt that matches the song's genre, vocal arrangement, tempo, and instrumentation.

## When to Use This Skill

Trigger this skill when users request:
- Telugu Christian song lyrics
- Telugu worship or praise songs
- Telugu devotional songs about Jesus, God, salvation
- Songs formatted for Suno AI in Telugu
- Christian songs in Telugu language

## Core Workflow

1. **Ask lyric questions FIRST** — single `AskUserQuestion` call with the four lyric questions in "Required Lyric Questions". Skip any the user already answered explicitly.
2. **Ask music production questions SECOND** — single `AskUserQuestion` call with the four music questions in "Required Music Questions". Skip any the user already answered explicitly.
3. **Generate Telugu lyrics** — based on the lyric answers and the patterns below.
4. **Generate the Suno style-of-music prompt** — based on the music answers; one cohesive English sentence tailored for Suno's "Style of Music" field.
5. **Format for Suno AI** — `[Verse]`, `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[End]` only.
6. **Save to file** — see "Output File Format". File goes in `created songs/`.

If the user has already given enough information for both batches in their original message, you MAY skip the questions entirely and go straight to generation. Never ask questions you already have answers to.

## Required Lyric Questions (Batch 1, ask via AskUserQuestion)

Send a single `AskUserQuestion` call with these four questions. Drop any the user already specified.

**Question 1 — Theme** (header: `Theme`)
- Worship & Praise (స్తుతి) — God's glory, majesty, holiness
- Jesus & Salvation (రక్షణ) — the cross, redemption, the blood
- Thanksgiving (కృతజ్ఞత) — gratitude for blessings and answered prayer
- God's Love & Grace (కృప / ప్రేమ) — divine love, mercy, transformation

**Question 2 — Telugu Style** (header: `Telugu Style`)
- Traditional / formal Telugu — classical worship vocabulary, devotional tone
- Contemporary / modern Telugu — accessible everyday phrasing, modern worship feel

**Question 3 — Length** (header: `Length`)
- Standard — 2 verses + 3 choruses + bridge (most common) — Recommended
- Simple — 2 verses + 2 choruses (shorter)
- Extended — 2 verses + pre-choruses + 3 choruses + bridge (longer, elaborate)

**Question 4 — Mood** (header: `Mood`)
- Joyful & Celebratory — upbeat, declarative, victorious
- Reflective & Devotional — intimate, prayerful, surrendered
- Powerful & Anthemic — bold, declaration of faith, prophetic

## Required Music Questions (Batch 2, ask via AskUserQuestion)

After the user answers the lyric batch, send a second `AskUserQuestion` call with these four questions. Drop any the user already specified.

**Question 1 — Music Genre** (header: `Genre`)
- Contemporary Worship — modern worship band: piano, electric guitar, ambient pads, drums
- Traditional Hymn / Gospel — choir-led, organ or piano, classic hymn feel
- Indian Devotional Fusion — harmonium, tabla, flute, sitar accents; bhajan-meets-worship
- Soft Acoustic Ballad — fingerpicked guitar or solo piano, intimate
- Anthemic Worship Rock — full band, strong drums, big chorus build

**Question 2 — Vocal Arrangement** (header: `Vocals`)
- Male solo lead
- Female solo lead
- Mixed duet — male and female trading lines
- Choir / group vocals with a lead

**Question 3 — Tempo** (header: `Tempo`)
- Medium (80–110 BPM) — flowing worship — Recommended
- Slow (60–80 BPM) — meditative, ballad-like
- Upbeat (110–130 BPM) — celebratory, danceable
- Fast (130+ BPM) — high energy, dynamic

**Question 4 — Featured Instruments** (header: `Instruments`, **multiSelect: true**)
- Piano
- Acoustic guitar
- Electric guitar
- Strings / pads (violin, cello, ambient strings)
- Drums / percussion
- Tabla / Indian percussion
- Harmonium
- Flute / bansuri
- Choir / backing vocals

After collecting both batches of answers, proceed to generate the song. Do not ask the user to confirm the plan — write the lyrics and style prompt directly.

### Sensible Defaults (for matching genre to instruments)

If the user's instrument choices clash with the genre, prefer the genre choice and note it. Reasonable defaults when the user is silent:

| Genre | Default instruments | Default tempo |
|-------|---------------------|---------------|
| Contemporary Worship | Piano, electric guitar, drums, strings/pads | Medium |
| Traditional Hymn / Gospel | Piano or organ, choir, light strings | Medium-slow |
| Indian Devotional Fusion | Harmonium, tabla, flute, soft acoustic guitar | Medium |
| Soft Acoustic Ballad | Acoustic guitar OR piano, light strings | Slow |
| Anthemic Worship Rock | Electric guitar, drums, bass, piano, choir | Upbeat |

## Telugu Christian Song Characteristics

### Common Themes
- **Worship & Praise** (స్తుతి - stuti): Praising God's glory, majesty, holiness
- **Jesus & Salvation** (రక్షణ - rakshana): Jesus Christ, the cross, redemption
- **Thanksgiving** (కృతజ్ఞత - krutagnata): Gratitude for God's blessings
- **God's Love & Grace** (కృప - krupa, ప్రేమ - prema): Divine love, mercy, grace

### Essential Vocabulary

Use these Telugu words naturally throughout the lyrics:

**Names and Titles:**
- యేసయ్యా (Yesayya) - Jesus
- దేవా (Deva) - God
- ప్రభువు (Prabhuvu) - Lord
- రాజా (Raja) - King
- రక్షకుడు (Rakshakudu) - Savior

**Worship Terms:**
- స్తుతి (Stuti) - Praise
- ఆరాధన (Aradhana) - Worship
- మహిమ (Mahima) - Glory
- హల్లెలూయ (Halleluya) - Hallelujah
- కీర్తన (Keertana) - Song of praise

**Spiritual Concepts:**
- కృప (Krupa) - Grace
- ప్రేమ (Prema) - Love
- రక్షణ (Rakshana) - Salvation
- విజయము (Vijayamu) - Victory
- శాంతి (Shanti) - Peace
- ఆశీర్వాదము (Aseervadamu) - Blessing
- సిలువ (Siluva) - Cross
- రక్తము (Raktamu) - Blood

### Language Style

Match the Telugu style answer:
- **Traditional / formal:** classical vocabulary, ornate metaphor, formal verb endings (నిలుచుచున్నాను, అనుగ్రహించుము)
- **Contemporary / modern:** everyday phrasing, conversational verb forms, accessible language

Always:
- Use poetic devices (alliteration, repetition)
- Include biblical imagery and metaphors
- Use direct address to God/Jesus (నీవు, నీ)
- Create natural rhyming patterns where possible

### Song Structure Guidelines

**Do NOT include [Intro] or [Outro] sections.** Always start with [Verse 1] and end with [End] immediately after the final [Chorus].

**Simple Structure:**
- [Verse 1] → [Chorus] → [Verse 2] → [Chorus] → [End]

**Standard Structure:**
- [Verse 1] → [Chorus] → [Verse 2] → [Chorus] → [Bridge] → [Chorus] → [End]

**Extended Structure:**
- [Verse 1] → [Pre-Chorus] → [Chorus] → [Verse 2] → [Pre-Chorus] → [Chorus] → [Bridge] → [Chorus] → [End]

### Section Guidelines

**[Verse]** — 4–8 lines, develops the theme, builds toward chorus. Verse 1 opens strong (no separate Intro).
**[Chorus]** — 4–6 lines, repetitive and memorable, often contains the song's title or key phrase.
**[Bridge]** — 2–4 lines, contrast and elevation, often more declarative or prophetic.
**[End]** — Closing marker on its own line. No content follows.

## Generating the Suno Style-of-Music Prompt

Compose ONE concise English sentence (or two short sentences) that Suno will read in its "Style of Music" field. Include, in this order:

1. **Genre / overall feel** — e.g., "Indian devotional fusion worship", "contemporary Christian worship ballad"
2. **Vocal arrangement** — e.g., "female solo lead with male backing harmonies", "male lead with choir"
3. **Language** — always include "Telugu vocals"
4. **Tempo** — e.g., "medium tempo around 95 BPM"
5. **Key instruments** — 3–5 of the user's selected instruments, no more
6. **Mood adjective** — match the lyric mood: "reverent and reflective", "joyful and celebratory", "powerful and anthemic"

**Example style prompt:**
> Indian devotional fusion worship with Telugu vocals, female solo lead and soft choir backing, medium tempo around 95 BPM, harmonium, tabla, soft acoustic guitar, flute, and ambient strings, reverent and reflective devotional tone.

Keep it under 50 words. No quotation marks, no embedded section tags.

## Output File Format

The output `.txt` file has TWO labeled sections separated by a blank line. The first section is the Suno style prompt; the second is the lyrics. The user pastes each into the matching Suno field.

```
=== SUNO STYLE PROMPT (paste into "Style of Music" field) ===
<one cohesive English sentence per the rules above>

=== LYRICS (paste into "Lyrics" field) ===
[Verse 1]
Telugu lyrics line 1
Telugu lyrics line 2
Telugu lyrics line 3
Telugu lyrics line 4

[Chorus]
...

[Verse 2]
...

[Chorus]
...

[Bridge]
...

[Chorus]
...
[End]
```

## Important Guidelines

1. **Authenticity** — lyrics must sound natural to Telugu Christian worship tradition.
2. **Theological soundness** — align with mainstream Christian biblical teaching.
3. **Singability** — phrases flow easily when sung.
4. **No musical directions inside the lyrics** — never embed `(soft piano)`, `(guitar solo)`, `(tabla fill)` between or inside verses. All production notes go in the top "Style of Music" block.
5. **Proper Telugu script** — use తెలుగు, not transliteration.
6. **Telugu vocals always declared** — the style prompt must explicitly say "Telugu vocals".
7. **No [Intro] or [Outro]** — begin with `[Verse 1]`, close with `[End]` immediately after the last `[Chorus]`.
8. **File naming** — `telugu_christian_song_<theme-slug>_<timestamp>.txt`.
9. **File location** — always save to `created songs/` (relative to project root). Never the project root itself.

## Example Workflow

**Example 1 — user gives no details: "Write me a Telugu Christian song"**

1. Call `AskUserQuestion` (Batch 1: Theme, Telugu Style, Length, Mood).
2. Call `AskUserQuestion` (Batch 2: Genre, Vocals, Tempo, Instruments).
3. Generate Telugu lyrics + matching Suno style prompt.
4. Save to `created songs/telugu_christian_song_worship_<timestamp>.txt`.

**Example 2 — user pre-specifies lyric details: "Generate a contemporary Telugu Christian song about God's grace, medium length"**

1. Theme (grace), Telugu Style (contemporary), Length (Standard) given. Ask only Mood in Batch 1.
2. Ask all four music questions in Batch 2.
3. Generate, format, save.

**Example 3 — user fully specifies: "Reflective traditional Telugu song about thanksgiving, simple structure, female solo lead with harmonium and tabla, slow tempo, Indian devotional fusion"**

1. All lyric and music answers present. Skip both `AskUserQuestion` calls.
2. Generate, format, save.

## Tips for Quality Lyrics

- **Start strong**: open with a compelling image or declaration.
- **Build progression**: each verse should deepen the theme.
- **Make chorus memorable**: use repetition and powerful imagery.
- **Use biblical references**: incorporate scriptural concepts naturally.
- **End with impact**: conclude with affirmation or declaration of faith.

## Tips for Quality Style Prompts

- **Be concrete**: "harmonium and tabla" beats "Indian instruments".
- **Match mood to tempo**: don't say "meditative" with "fast tempo".
- **Don't list every instrument** — pick the 3–5 most defining ones; Suno does best with focused descriptions.
- **Always name the language** — "Telugu vocals" anchors Suno to the right phonetic model.

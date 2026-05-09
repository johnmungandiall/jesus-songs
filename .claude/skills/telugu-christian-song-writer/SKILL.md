---
name: telugu-christian-song-writer
description: Generate original Telugu Christian song lyrics formatted for Suno AI. Use this skill whenever the user asks to create, write, or generate Telugu Christian songs, Telugu worship songs, Telugu praise songs, or Telugu devotional songs. Also trigger when users mention Suno AI format with Telugu Christian content, or ask for song lyrics about Jesus, God, salvation, worship, or praise in Telugu language.
---

# Telugu Christian Song Writer for Suno AI

Generate authentic Telugu Christian song lyrics formatted for Suno AI music generation platform.

## When to Use This Skill

Trigger this skill when users request:
- Telugu Christian song lyrics
- Telugu worship or praise songs
- Telugu devotional songs about Jesus, God, salvation
- Songs formatted for Suno AI in Telugu
- Christian songs in Telugu language

## Core Workflow

1. **Ask selectable questions FIRST** - Use the `AskUserQuestion` tool to gather the user's preferences before writing anything (see "Required Questions" below). Skip any question the user has already answered explicitly in their message.
2. **Generate Telugu lyrics** - Create authentic Telugu Christian lyrics based on the answers and the patterns below
3. **Format for Suno AI** - Structure with proper tags ([Verse], [Chorus], [Bridge], [End])
4. **Save to file** - Write the formatted lyrics to a .txt file

## Required Questions (ask via AskUserQuestion)

Before generating the song, send a single `AskUserQuestion` call with the four questions below. If the user already specified one or more of these in their request (e.g., "write a contemporary song about grace"), drop those questions and only ask the remaining ones.

**Question 1 — Theme** (header: `Theme`)
- Worship & Praise (స్తుతి) — God's glory, majesty, holiness
- Jesus & Salvation (రక్షణ) — the cross, redemption, the blood
- Thanksgiving (కృతజ్ఞత) — gratitude for blessings and answered prayer
- God's Love & Grace (కృప / ప్రేమ) — divine love, mercy, transformation

**Question 2 — Style** (header: `Style`)
- Traditional / formal Telugu — classical worship vocabulary, devotional tone
- Contemporary / modern Telugu — accessible everyday phrasing, modern worship feel

**Question 3 — Length** (header: `Length`)
- Simple — 2 verses + 2 choruses (shorter)
- Standard — 2 verses + 3 choruses + bridge (most common) — Recommended
- Extended — 2 verses + pre-choruses + 3 choruses + bridge (longer, elaborate)

**Question 4 — Mood** (header: `Mood`)
- Joyful & Celebratory — upbeat, declarative, victorious
- Reflective & Devotional — intimate, prayerful, surrendered
- Powerful & Anthemic — bold, declaration of faith, prophetic

After collecting answers, proceed to generate the song. Do not ask the user to confirm the plan — write the lyrics directly.

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

Write in a mix of formal and contemporary Telugu:
- Use poetic devices like alliteration and repetition
- Include biblical imagery and metaphors
- Maintain emotional and devotional tone
- Use direct address to God/Jesus (నీవు - neevu, నీ - nee)
- Create natural rhyming patterns where possible

### Song Structure Guidelines

Choose structure based on the theme and user preference. **Do NOT include [Intro] or [Outro] sections.** Always start with [Verse 1] and end with [End] immediately after the final [Chorus].

**Simple Structure** (shorter songs):
- [Verse 1]
- [Chorus]
- [Verse 2]
- [Chorus]
- [End]

**Standard Structure** (most common):
- [Verse 1]
- [Chorus]
- [Verse 2]
- [Chorus]
- [Bridge]
- [Chorus]
- [End]

**Extended Structure** (longer, more elaborate):
- [Verse 1]
- [Pre-Chorus]
- [Chorus]
- [Verse 2]
- [Pre-Chorus]
- [Chorus]
- [Bridge]
- [Chorus]
- [End]

### Section Guidelines

**[Verse]**
- Tell the story or develop the theme
- 4-8 lines typically
- Build toward the chorus
- Each verse should progress the message
- Verse 1 should open strong with a compelling image or declaration (no separate Intro)

**[Chorus]**
- The main message and hook
- Repetitive and memorable
- 4-6 lines typically
- Should be singable and emotionally powerful
- Often includes the song's title or key phrase

**[Bridge]**
- Provides contrast and elevation
- 2-4 lines typically
- Intensifies the message
- Often more declarative or prophetic

**[End]**
- Place immediately after the final [Chorus] on its own line
- No content follows — it is a closing marker, not a section with lyrics

## Output Format

Format the lyrics exactly like this for Suno AI. **No [Intro], no [Outro] — start with [Verse 1] and end with [End] right after the final [Chorus].**

```
[Verse 1]
Telugu lyrics line 1
Telugu lyrics line 2
Telugu lyrics line 3
Telugu lyrics line 4

[Chorus]
Telugu lyrics line 1
Telugu lyrics line 2
Telugu lyrics line 3
Telugu lyrics line 4

[Verse 2]
Telugu lyrics line 1
Telugu lyrics line 2
Telugu lyrics line 3
Telugu lyrics line 4

[Chorus]
Telugu lyrics line 1
Telugu lyrics line 2
Telugu lyrics line 3
Telugu lyrics line 4

[Bridge]
Telugu lyrics line 1
Telugu lyrics line 2
Telugu lyrics line 3
Telugu lyrics line 4

[Chorus]
Telugu lyrics line 1
Telugu lyrics line 2
Telugu lyrics line 3
Telugu lyrics line 4
[End]
```

## Important Guidelines

1. **Authenticity**: Write lyrics that sound natural to Telugu Christian worship tradition
2. **Theological soundness**: Ensure lyrics align with Christian biblical teachings
3. **Emotional resonance**: Create lyrics that inspire worship, devotion, and connection with God
4. **Singability**: Keep phrases flowing and easy to sing
5. **No musical directions**: Do NOT include parenthetical musical notes like "(Soft piano)" or "(Guitar solo)" - focus only on Telugu lyrics
6. **Proper Telugu script**: Always use Telugu script (తెలుగు), not transliteration
7. **File naming**: Save as `telugu_christian_song_[theme]_[timestamp].txt`
8. **No [Intro] or [Outro]**: Always begin with [Verse 1] and close with `[End]` immediately after the last [Chorus]. Do not add any sections or lines outside of [Verse], [Pre-Chorus], [Chorus], [Bridge], and the final [End] marker.

## Example Workflow

**Example 1 — user gives no details: "Write me a Telugu Christian song"**

1. Call `AskUserQuestion` with all four questions (Theme, Style, Length, Mood)
2. Receive answers, e.g., Worship & Praise / Contemporary / Standard / Joyful
3. Generate Telugu lyrics matching those choices
4. Format with Suno AI tags ([Verse 1] → [Chorus] → ... → [End])
5. Save to file: `telugu_christian_song_worship_[timestamp].txt`

**Example 2 — user pre-specifies some details: "Generate a contemporary Telugu Christian song about God's grace, medium length"**

1. User already gave Theme (grace), Style (contemporary), Length (medium → Standard). Only Mood is missing.
2. Call `AskUserQuestion` with **only** the Mood question
3. Generate Telugu lyrics on God's grace, contemporary style, standard structure, with the chosen mood
4. Save to file: `telugu_christian_song_gods_grace_[timestamp].txt`

**Example 3 — user gives full details: "Reflective traditional Telugu song about thanksgiving, simple structure"**

1. All four answers are present in the request — skip `AskUserQuestion` entirely
2. Go straight to generating the lyrics

## Tips for Quality Lyrics

- **Start strong**: Open with a compelling image or declaration
- **Build progression**: Each verse should deepen the theme
- **Make chorus memorable**: Use repetition and powerful imagery
- **Use biblical references**: Incorporate scriptural concepts naturally
- **Maintain consistency**: Keep the theme focused throughout
- **End with impact**: Conclude with affirmation or declaration of faith

## Handling User Requests

If user specifies:
- **Theme**: Focus lyrics on that specific theme
- **Style**: Adjust between traditional (formal Telugu) or contemporary (modern expressions)
- **Length**: Adjust number of verses and structure complexity
- **Specific words/phrases**: Incorporate their requested Telugu words or concepts

If user doesn't specify details, create a balanced worship song with standard structure focusing on praise and worship themes.

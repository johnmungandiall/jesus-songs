---
name: telugu-christian-song-writer
description: Generate original Telugu Christian song lyrics formatted for Suno AI, with a matching Suno style-of-music prompt covering genre, vocals, tempo, and instruments. Use this skill whenever the user asks to create, write, or generate Telugu Christian songs, Telugu worship songs, Telugu praise songs, or Telugu devotional songs. Also trigger when users mention Suno AI format with Telugu Christian content, or ask for song lyrics about Jesus, God, salvation, worship, or praise in Telugu language.
---

# Telugu Christian Song Writer for Suno AI

Generate authentic Telugu Christian song lyrics in the **pallavi-charanam tradition** (Carnatic-influenced structure used by virtually all Telugu Christian songs at sites like christianlyricz.com, jesuslyricz.in, waytochurch.com, uecf.net). Output is formatted for Suno AI with a matched "Style of Music" prompt covering genre, vocal arrangement, tempo, and instrumentation.

## When to Use This Skill

Trigger this skill when users request:
- Telugu Christian song lyrics
- Telugu worship, praise, prayer, thanksgiving, comfort, repentance, gospel, Christmas, Easter, Good Friday, or Second Coming songs
- Songs formatted for Suno AI in Telugu
- Christian songs in Telugu language

## Core Workflow

1. **Ask lyric questions FIRST** — single `AskUserQuestion` call with the four lyric questions in "Required Lyric Questions". Skip any the user already answered explicitly.
2. **Ask music production questions SECOND** — single `AskUserQuestion` call with the four music questions in "Required Music Questions". Skip any the user already answered explicitly.
3. **Generate Telugu lyrics** following the pallavi-charanam template in "Song Structure".
4. **Generate the Suno style-of-music prompt** based on the music answers; one cohesive English sentence tailored for Suno's "Style of Music" field.
5. **Format for Suno AI** — `[Verse]`, `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[End]` only.
6. **Save to file** — see "Output File Format". File goes in `created songs/`.

If the user has already given enough information for both batches in their original message, skip the questions entirely and go straight to generation. Never ask questions you already have answers to.

## Required Lyric Questions (Batch 1, ask via AskUserQuestion)

Send a single `AskUserQuestion` call with these four questions. Drop any the user already specified.

**Question 1 — Theme** (header: `Theme`)
- Worship & Praise (స్తుతి / ఆరాధన) — God's glory, majesty, holiness, name
- Jesus & Salvation (రక్షణ / సిలువ) — the cross, the blood, redemption (Easter / Good Friday flavors)
- Thanksgiving (కృతజ్ఞత / స్తోత్రం) — gratitude for blessings, faithful protection (Ebenezer-style)
- God's Love & Grace (కృప / ప్రేమ) — divine love, mercy, transformation
- Prayer & Surrender (ప్రార్థన / సమర్పణ) — petition, devotion, "you alone are mine"
- Comfort & Hope (ఓదార్పు / ఆశ) — God in trials, refuge, future glory
- Second Coming & Heaven (రాకడ / పరలోకము) — eschatological hope, the bride awaiting
- Narrative Praise (Bible-hero stories) — Moses, Joshua, Daniel, Paul & Silas style

**Question 2 — Telugu Style** (header: `Telugu Style`)
- Traditional / formal Telugu — classical worship vocabulary (స్తుతియించుడి, దేవా, యెహోవా, శాశ్వతమైనది), verb endings like -చితివి, -యించుచున్నాను; old-Andhra hymnal feel
- Contemporary / modern Telugu — accessible everyday phrasing (నీ ప్రేమ, నువ్వే, యేసయ్యా), modern worship feel à la Hosanna Ministries / Krupasanam-era
- Devotional-poetic — Song-of-Solomon imagery (షారోను పుష్పం, లోయలోని పద్మం), intimate "నా ప్రియుడా" register

**Question 3 — Length** (header: `Length`)
- Standard — 1 pallavi + 3 charanams (matches most published Telugu Christian songs) — Recommended
- Short — 1 pallavi + 2 charanams (compact)
- Extended — 1 pallavi + 4–5 charanams + bridge (long-form hymn or narrative praise)

**Question 4 — Mood** (header: `Mood`)
- Joyful & Celebratory — upbeat, declarative, victorious (హల్లెలూయా, స్తుతియించుడి)
- Reflective & Devotional — intimate, prayerful, surrendered (నా ప్రియుడా, నీ సన్నిధిలో)
- Powerful & Anthemic — bold, declaration of faith, prophetic (రాజుల రాజా, విజయము)
- Sorrowful & Repentant — Good Friday, lament, gratitude for the cross (మరువలేను, పంచగాయములు)

## Required Music Questions (Batch 2, ask via AskUserQuestion)

After the user answers the lyric batch, send a second `AskUserQuestion` call with these four questions. Drop any the user already specified.

**Question 1 — Music Genre** (header: `Genre`)
- Contemporary Worship — modern worship band: piano, electric guitar, ambient pads, drums
- Traditional Hymn / Andhra Christian Keertana — choir-led, organ or piano, classic Andhra hymn feel
- Indian Devotional Fusion — harmonium, tabla, flute, sitar accents; bhajan-meets-worship
- Soft Acoustic Ballad — fingerpicked guitar or solo piano, intimate
- Anthemic Worship Rock — full band, strong drums, big chorus build
- Carnatic-tinged Worship — violin, mridangam, harmonium, classical melodic ornaments

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
- Mridangam
- Harmonium
- Flute / bansuri
- Veena / sitar
- Choir / backing vocals

After collecting both batches of answers, proceed to generate the song. Do not ask the user to confirm the plan — write the lyrics and style prompt directly.

### Sensible Defaults (matching genre to instruments)

If the user's instrument choices clash with the genre, prefer the genre choice and note it. Reasonable defaults when the user is silent:

| Genre | Default instruments | Default tempo |
|-------|---------------------|---------------|
| Contemporary Worship | Piano, electric guitar, drums, strings/pads | Medium |
| Traditional Hymn / Andhra Keertana | Piano or organ, choir, light strings | Medium-slow |
| Indian Devotional Fusion | Harmonium, tabla, flute, soft acoustic guitar | Medium |
| Soft Acoustic Ballad | Acoustic guitar OR piano, light strings | Slow |
| Anthemic Worship Rock | Electric guitar, drums, bass, piano, choir | Upbeat |
| Carnatic-tinged Worship | Violin, mridangam, harmonium, flute | Medium |

## Telugu Christian Song Structure (Pallavi-Charanam Tradition)

Real Telugu Christian songs are built on the **pallavi (పల్లవి) → charanam (చరణం)** pattern inherited from Carnatic music. **The song opens with the pallavi (the title hook), not with a verse.** Map this to Suno tags as:

| Telugu term | Function | Suno tag |
|------------|----------|----------|
| Pallavi (పల్లవి) | Opening hook + main refrain — contains the song's title phrase | `[Chorus]` (placed first) |
| Anupallavi (అనుపల్లవి) | Optional secondary hook bridging pallavi to charanam | `[Pre-Chorus]` |
| Charanam (చరణం) | Verse — develops the theme; usually ends by leading back to pallavi | `[Verse N]` |
| Concluding charanam | Final declarative verse, often more prophetic | `[Bridge]` |

### Standard structure (use this by default)

```
[Chorus]      ← pallavi: title hook, sung first to anchor the song
[Verse 1]     ← charanam 1
[Chorus]
[Verse 2]     ← charanam 2
[Chorus]
[Verse 3]     ← charanam 3 (or [Bridge] if more declarative/prophetic)
[Chorus]
[End]
```

### Short structure

```
[Chorus] → [Verse 1] → [Chorus] → [Verse 2] → [Chorus] → [End]
```

### Extended structure

```
[Chorus] → [Verse 1] → [Pre-Chorus] → [Chorus] → [Verse 2] → [Pre-Chorus] → [Chorus]
        → [Verse 3] → [Chorus] → [Bridge] → [Chorus] → [End]
```

**Do NOT use `[Intro]` or `[Outro]`.** Opening with `[Chorus]` is not an intro — it is the pallavi, the authentic Telugu Christian song opening. End with `[End]` immediately after the final `[Chorus]`.

### Section length guidelines

- **[Chorus] / pallavi** — 4 lines, often built as 2 rhyming couplets. Contains the song's title/hook phrase, usually as the first line. Memorable and singable. Often opens with a vocative (యేసయ్యా / యెహోవా / దేవా / రాజా / సుందరుడా).
- **[Verse] / charanam** — 4–6 lines, develops the theme. Usually 2 rhyming couplets ending with a phrase that leads emotionally back into the chorus.
- **[Pre-Chorus]** (optional) — 2 lines, builds tension before the chorus.
- **[Bridge]** — 2–4 lines, contrast and elevation. Often uses chains of "నీవే ... నీవే ..." (You alone are ...) declarations.
- **[End]** — closing marker on its own line. No content follows.

### Repetition convention (CRITICAL for Suno)

Traditional Telugu lyric sheets use compact repetition markers — `(2)` for "sing twice" and `||హుక్|| ` to mean "return to the pallavi labeled by these words". **Suno cannot read these markers.** You must:

- **Expand all repetitions inline.** If a line is sung twice, write it twice. If the chorus repeats, write the full `[Chorus]` block again.
- Never include `(2)`, `(3)`, `||...||`, or any other shorthand.
- Use Suno section tags (`[Chorus]`, `[Verse 1]`, etc.) to drive the actual repetition; Suno will perform each tagged section.

## Telugu Christian Vocabulary (use naturally)

### Names and Titles for God / Jesus
- యేసయ్యా (Yesayyaa) — Jesus (intimate vocative)
- యేసు (Yesu) — Jesus
- యెహోవా (Yehovaa) — Jehovah / LORD
- దేవా (Devaa) — God (vocative)
- దేవుడు (Devudu) — God
- ప్రభువా / ప్రభువు (Prabhuvaa / Prabhuvu) — Lord
- తండ్రీ / తండ్రి (Tandri) — Father
- రాజా / రాజు (Rajaa / Raju) — King
- రాజుల రాజు (Rajula Raju) — King of kings
- రక్షకుడు (Rakshakudu) — Savior
- దయామయా (Dayaamayaa) — Merciful One
- సర్వశక్తుడా (Sarvashaktudaa) — Almighty
- మహోన్నతుడా (Mahonnatudaa) — Most High
- సుందరుడా (Sundarudaa) — Beautiful One
- అతిశయుడా (Atishayudaa) — Wondrous / Excellent One
- ప్రియుడా (Priyudaa) — Beloved
- క్రీస్తు (Kreesthu) — Christ
- ఎబినేజరు (Ebinejaru) — Ebenezer ("stone of help")
- ఇమ్మానుయేలు (Immaanuyelu) — Immanuel
- నాథుడు (Naathudu) — Lord / Master
- దైవ తనయా (Daiva Thanayaa) — Son of God

### Worship terms
- స్తుతి (Stuti) — praise
- స్తోత్రం (Stotram) — thanksgiving / praise offering
- స్తుతియించుడి (Stutiyinchudi) — "praise Him!" (formal hortative)
- ఆరాధన (Aaraadhana) — worship
- మహిమ (Mahima) — glory
- హల్లెలూయా (Halleluyaa) — Hallelujah
- కీర్తన (Keertana) — song of praise
- ఆమెన్ (Aamen) — Amen
- సన్నిధి (Sannidhi) — presence (of God)
- సింహాసనము (Simhaasanamu) — throne

### Salvation / cross imagery
- సిలువ (Siluva) — cross
- రక్తము / రుధిరం (Raktamu / Rudhiram) — blood
- బలి (Bali) — sacrifice
- పాపము (Paapamu) — sin
- క్షమ (Kshama) — forgiveness
- రక్షణ (Rakshana) — salvation
- విమోచన (Vimochana) — redemption
- పంచగాయములు (Panchagaayamulu) — the five wounds
- ముళ్ళకిరీటం (Mullakireetam) — crown of thorns
- కల్వరి (Kalvari) — Calvary
- సమాధి (Samaadhi) — tomb / grave
- పునరుత్థానం (Punarutthaanam) — resurrection

### Spiritual concepts
- కృప (Krupa) — grace
- ప్రేమ (Prema) — love
- విజయము (Vijayamu) — victory
- శాంతి (Shanti) — peace
- ఆశీర్వాదము (Aaseervaadamu) — blessing
- దీవెన (Deevena) — blessing
- అనుగ్రహం (Anugraham) — favor / grace
- నమ్మకం (Nammakam) — faith / trust
- ఆశ (Aasha) — hope
- నిత్యజీవము (Nityajeevamu) — eternal life
- శాశ్వతమైనది (Saashvatamainadi) — eternal
- పరలోకము (Paralokamu) — heaven
- సంఘము (Sanghamu) — church / congregation
- సాక్షి (Saakshi) — witness
- మార్గము / దారి (Maargamu / Daari) — way / path
- సత్యము (Satyamu) — truth
- జీవము (Jeevamu) — life
- వెలుగు (Velugu) — light

### Biblical imagery used in real Telugu songs
- షారోను పుష్పం (Sharon Pushpam) — Rose of Sharon
- లోయలోని పద్మం (Loyaloni Padmam) — Lily of the Valley
- అగ్ని స్తంభం (Agni Stambham) — pillar of fire
- మేఘ స్తంభం (Megha Stambham) — pillar of cloud
- సెలయేరు (Selayeru) — flowing stream / brook
- కనుపాప (Kanupaapa) — apple of the eye
- కౌగిలి (Kaugili) — embrace
- ఎడారి (Edaari) — desert / wilderness
- మన్నా (Mannaa) — manna
- కన్నతండ్రి / కన్నతల్లి (Kannatandri / Kannatalli) — birth-father / birth-mother (used metaphorically for God's tenderness)
- బలమైన బురుజు (Balamaina Buruju) — strong tower

### Biblical heroes for narrative-praise songs
మోషే (Moshe / Moses), యెహోషువా (Yehoshuvaa / Joshua), దానియేలు (Daaniyelu / Daniel), షద్రకు (Shadraku / Shadrach), మెషాకు (Meshaaku / Meshach), అబేద్నెగో (Abednego), పౌలు (Paulu / Paul), సీల (Seela / Silas), దావీదు (Daaveedu / David), యోనా (Yonaa / Jonah), ఎలీయా (Eleeyaa / Elijah).

## Telugu Poetic Devices for Authentic Sound

Real Telugu Christian songs use these signature devices — incorporate them:

1. **Vocative anchoring** — open the pallavi with a vocative call: "యేసయ్యా...", "యెహోవా...", "దేవా...", "రాజా...", "సుందరుడా...". Often repeated 2x or 3x.
2. **Sustained vowel interjections** — "ఆ…ఆ…ఆ…" or "ఓ ఓ ఓ…" between or inside chorus lines for melismatic worship feel. Use sparingly, mainly in the pallavi.
3. **Perfective divine-action endings** — verbs in -తివే / -తివి / -చితివి / -నావే describe God's completed acts ("you protected", "you became"). These give the lyric a worshipful "looking back at what God did" tone. Examples: కాచితివే, నడిపించితివి, చేసితివే, ఇచ్చావే.
4. **Pause-dot phrasing** — within long lines, use ".." (double dots) to mark short sung pauses: "దారులలో.. ఎడారులలో.. సెలయేరులై ప్రవహించుమయా". This is conventional Telugu Christian lyric notation.
5. **End-rhyme couplets (AABB)** — pair lines so they end with the same sound: e.g., -యా/-యా, -వే/-వే, -తివే/-తివే.
6. **Anaphora (repeated openings)** — repeat the opening word of consecutive lines: "నీవే మార్గము / నీవే సత్యము / నీవే జీవము".
7. **Triple-attribute strings** — chain three or four divine attributes in one line: "సుందరుడా… అతిశయుడా… మహోన్నతుడా… నా ప్రియుడా".
8. **Direct address (నీవు / నీ)** — speak TO God in second person; avoid third-person narration unless quoting Scripture.
9. **Honorific suffix "-యా"** added to vocatives ("యేసయ్యా") for tenderness. Use freely in contemporary style; sparingly in formal hymn style.

## Pattern Templates (reference, not for direct copying)

These are abstract patterns observed across multiple published Telugu Christian songs. Use them as scaffolding, not as text to copy.

**Pallavi pattern A — vocative + attribute string** (worship/devotional):
```
[Vocative]… [Attribute 1]…
[Attribute 2]… నా [Attribute 3]
[Vocative]… [Attribute 1]…
[Attribute 2]… నా [Attribute 3]
```

**Pallavi pattern B — declarative truth + Hallelujah** (praise/hymn):
```
[Subject about God] ఎంతో [adjective]
ఆ…ఆ…ఆ… ఎంతో [adjective]
[Restatement with different name] ఎంతో [adjective]
హల్లెలూయా దేవుని స్తుతియించుడి
```

**Charanam pattern — narrative + return cue**:
```
[Two lines describing a divine act, ending in -తివే / -చితివి]
[Two lines responding with praise or testimony]
[Optional: lead-back line ending in -యా / -నయ్యా]
```

**Bridge pattern — "you alone" chain**:
```
నీవే మార్గము — నీవే సత్యము
నీవే జీవము — నా సర్వము నీవే
```

## Generating the Suno Style-of-Music Prompt

Compose ONE concise English sentence (or two short sentences) for Suno's "Style of Music" field. Include, in this order:

1. **Genre / overall feel** — e.g., "Indian devotional fusion worship", "contemporary Telugu Christian worship ballad", "traditional Andhra Christian hymn"
2. **Vocal arrangement** — e.g., "female solo lead with male backing harmonies", "male lead with choir"
3. **Language** — always include "Telugu vocals"
4. **Tempo** — e.g., "medium tempo around 95 BPM"
5. **Key instruments** — 3–5 of the user's selected instruments, no more
6. **Mood adjective** — match the lyric mood: "reverent and reflective", "joyful and celebratory", "powerful and anthemic", "sorrowful and grateful"

**Example style prompt:**
> Indian devotional fusion worship with Telugu vocals, female solo lead and soft choir backing, medium tempo around 95 BPM, harmonium, tabla, soft acoustic guitar, flute, and ambient strings, reverent and reflective devotional tone.

Keep it under 50 words. No quotation marks, no embedded section tags.

## Output File Format

The output `.txt` file has TWO labeled sections separated by a blank line. The user pastes each block into the matching Suno field.

```
=== SUNO STYLE PROMPT (paste into "Style of Music" field) ===
<one cohesive English sentence per the rules above>

=== LYRICS (paste into "Lyrics" field) ===
[Chorus]
<pallavi: 4 lines, hook with song title>

[Verse 1]
<charanam 1: 4–6 lines>

[Chorus]
<repeat pallavi in full>

[Verse 2]
<charanam 2: 4–6 lines>

[Chorus]
<repeat pallavi in full>

[Verse 3]
<charanam 3 OR [Bridge] if more declarative>

[Chorus]
<repeat pallavi in full>
[End]
```

## Important Guidelines

1. **Authenticity** — lyrics must sound natural to the Telugu Christian worship tradition (pallavi-charanam structure, vocative openings, perfective divine-action verbs).
2. **Theological soundness** — align with mainstream Christian biblical teaching. Trinitarian. Christ-centered. No prosperity-gospel framing.
3. **Open with the chorus (pallavi)** — the song's first sung line must be the title hook, not a verse setup. This is a hard rule; every published Telugu Christian song does this.
4. **Singability** — phrases flow easily when sung. Read each line aloud; if it stumbles, simplify.
5. **No musical directions inside the lyrics** — never embed `(soft piano)`, `(guitar solo)`, `(tabla fill)` between or inside verses. All production notes go in the top "Style of Music" block.
6. **Proper Telugu script** — use తెలుగు script, not transliteration.
7. **Telugu vocals always declared** — the style prompt must explicitly say "Telugu vocals".
8. **No `[Intro]` or `[Outro]` tags** — opening with `[Chorus]` is the pallavi, not an intro. Close with `[End]` immediately after the last `[Chorus]`.
9. **No traditional repetition shorthand** — never write `(2)`, `(3)`, `||hook||`, or `||refrain||` in Suno output. Expand every repetition inline; let Suno tags drive section repeats.
10. **File naming** — `telugu_christian_song_<theme-slug>_<timestamp>.txt`.
11. **File location** — always save to `created songs/` (relative to project root). Never the project root itself.

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

**Example 4 — narrative praise: "Write a Telugu praise song about how God delivered Daniel and Paul-Silas"**

1. Detect "narrative praise" theme — each charanam should name one biblical hero and the deliverance miracle, ending with a return-to-pallavi praise line. Ask remaining lyric/music questions.
2. Use the "praise hymn" pallavi pattern with "హల్లెలూయా / స్తుతియించుడి".
3. Generate, format, save.

## Tips for Quality Lyrics

- **Open with the hook**: the very first line of the pallavi should contain the song's title phrase.
- **Build progression**: each charanam should deepen the theme (e.g., creation → cross → resurrection; or past deliverance → present help → future hope).
- **Make the chorus (pallavi) singable on first hearing**: short lines, vocative call, repeating sound.
- **Use biblical references**: incorporate scriptural concepts and imagery naturally (Sharon's Rose, pillar of fire, apple of the eye).
- **End with affirmation**: the final charanam or bridge should declare faith, not introduce a new question.
- **Match register to genre**: traditional hymn → formal verb endings (-చితివి, -యించుడి); contemporary worship → conversational endings (-చావు, -చావే).

## Tips for Quality Style Prompts

- **Be concrete**: "harmonium and tabla" beats "Indian instruments".
- **Match mood to tempo**: don't say "meditative" with "fast tempo".
- **Don't list every instrument** — pick the 3–5 most defining ones; Suno does best with focused descriptions.
- **Always name the language** — "Telugu vocals" anchors Suno to the right phonetic model.
- **For narrative praise / older hymn feel**, add "Andhra Christian keertana style" — Suno has seen this label.

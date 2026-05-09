# వాడుక మార్గదర్శి (Usage Guide)

ఈ ప్రాజెక్ట్‌లో తెలుగు క్రైస్తవ పాటలు Suno AI కోసం రాయడానికి, audit చేయడానికి, improve చేయడానికి కావలసిన commands మరియు skills ఇక్కడ వివరించబడ్డాయి.

---

## మొత్తం flow ఒక్క చూపులో

```
పాట rayadam → created songs/ లో save → Suno లో test → నచ్చితే tested/ కి move
```

పాట రాయడానికి **రెండు మార్గాలు** ఉన్నాయి:

| మార్గం | ఎప్పుడు వాడాలి |
|------|----------------|
| `/write-song-quick` | వేగంగా ఒక పాట కావాలి, ప్రశ్నలు వద్దు, smart defaults చాలు |
| `telugu-christian-song-writer` skill | theme, style, mood, instruments — అన్ని వివరాలపై మీ control కావాలి |

పాటలను review చేయడానికి:

| మార్గం | ఏం చేస్తుంది |
|------|------------|
| `/review-songs` | `created songs/` లోని పాటలను audit చేస్తుంది; సమస్యలు ఉంటే improved version తయారు చేస్తుంది |

---

## 1. `/write-song-quick` — వేగంగా ఒక పాట రాయడం

ఎలాంటి ప్రశ్నలు అడగకుండా, smart defaults తో ఒక పాట రాస్తుంది. మీరు ఒక theme line పాస్ చేస్తే, దానికి తగ్గట్టు mood adjust అవుతుంది.

### Default settings (override లేకపోతే)

- **Theme** — ఆరాధన మరియు స్తుతి (Worship & Praise)
- **Telugu Style** — Contemporary (ఆధునిక శైలి, యేసయ్యా / నీ ప్రేమ / నువ్వే)
- **Length** — Standard (1 పల్లవి + 3 చరణాలు)
- **Mood** — Reflective & Devotional (ధ్యానపరమైన, intimate)
- **Genre** — Contemporary Worship band
- **Tempo** — Medium 90–100 BPM
- **Instruments** — Piano, acoustic guitar, ambient strings, soft drums

### ఉదాహరణలు

```
/write-song-quick
/write-song-quick గ్రేస్ — దేవుని కృప మరియు దయ
/write-song-quick Good Friday — సిలువ మరియు రక్తం
/write-song-quick Daniel in the lions' den, narrative praise
/write-song-quick Christmas — యేసు జననం
```

Theme line లో "Good Friday" వంటి keywords ఇస్తే, agent automatic గా mood ను Sorrowful & Repentant కి switch చేస్తుంది. "narrative praise" అంటే charanam లలో biblical heroes గురించి కథ చెప్పేలా రాస్తుంది.

### Output ఎక్కడ?

`created songs/telugu_christian_song_<theme>_<timestamp>.txt`

File లో రెండు blocks ఉంటాయి — Suno కి paste చేయడానికి సిద్ధంగా.

---

## 2. `telugu-christian-song-writer` skill — interactive గా రాయడం

మీకు పూర్తి control కావాలంటే ఈ skill వాడండి. Skill మీకు **రెండు సెట్ల ప్రశ్నలు** అడుగుతుంది:

**Batch 1 — Lyric questions:**
- Theme (Worship / Salvation / Thanksgiving / Grace / Prayer / Comfort / Second Coming / Narrative Praise)
- Telugu Style (Traditional / Contemporary / Devotional-poetic)
- Length (Short / Standard / Extended)
- Mood (Joyful / Reflective / Anthemic / Sorrowful)

**Batch 2 — Music questions:**
- Genre (Contemporary Worship / Traditional Hymn / Indian Devotional Fusion / Acoustic Ballad / Anthemic Rock / Carnatic-tinged)
- Vocals (Male solo / Female solo / Mixed duet / Choir)
- Tempo (Slow / Medium / Upbeat / Fast)
- Instruments (multi-select)

మీరు original message లోనే ఈ details ఇస్తే, skill ప్రశ్నలు skip చేసి నేరుగా రాస్తుంది.

### Skill ను trigger ఎలా చేయాలి?

Claude Code session లో సాధారణంగా అడిగితే చాలు:

```
"Write me a Telugu Christian song about thanksgiving"
"తెలుగు క్రైస్తవ పాట రాయండి — Easter theme, traditional hymn style"
"Generate a worship song in Telugu with harmonium and tabla"
```

---

## 3. `/review-songs` — పాటలను audit చేయడం, మెరుగుపరచడం

`created songs/` లోని పాటలను నాలుగు dimensions లో score చేస్తుంది: Suno format, Telugu fluency, theology, singability.

### ఎలా run చేయాలి

```
/review-songs                                  ← created songs/ లోని అన్ని పాటలు
/review-songs created songs/my-song.txt        ← ఒక్క పాట
/review-songs created songs/*.txt              ← glob pattern
/review-songs styles/                          ← వేరే directory
```

### Two-phase pipeline

1. **Audit phase** — ప్రతి పాటకి ఒక `song-auditor` agent parallel గా run అవుతుంది. Reviews `.claude/agent-output/song-auditor/<song>-review.md` లో save అవుతాయి.
2. **Improve phase** — review లో `Recommended Action: Send to song-improver` అని ఉంటే, ఆ song కి `song-improver` agent run అవుతుంది. Improved version `.claude/agent-output/song-improver/<song>-improved.txt` లోకి వస్తుంది.

### ముఖ్యం — auto-promote ఉండదు

Improved songs ను agents **automatic గా `created songs/` లోకి copy చేయవు**. మీరే వాటిని review చేసి, నచ్చితే manually `created songs/` లోకి తీసుకోవాలి.

---

## 4. `styles/` library — 100 ready-to-paste Suno style prompts

కొత్త lyrics అవసరం లేకుండా Suno style prompt మాత్రమే కావాలంటే [styles/INDEX.md](styles/INDEX.md) చూడండి.

**16 folders, 100 styles:**
- `worship-contemporary/` — modern worship band (10)
- `worship-traditional/` — hymns, choir, organ (7)
- `praise-gospel/` — gospel celebration (10)
- `indian-fusion/` — bhajan, carnatic, harmonium-led (13)
- `acoustic-intimate/`, `electronic-modern/`, `hiphop-spoken/`, `jazz-sophisticated/`, `rock-band/`
- `occasion-christmas/`, `occasion-easter-good-friday/`, `occasion-wedding/`, `occasion-funeral/`, `occasion-kids/`, `occasion-sacraments/`, `occasion-special/`

ప్రతి file లో `=== SUNO STYLE PROMPT ===` heading కింద paste-ready prompt ఉంటుంది.

`south indian telugu styles/` folder లో music-director-flavored variants ఉన్నాయి (specific MD styles + song types).

---

## 5. File format — ప్రతి generated `.txt` ఇలా ఉంటుంది

```
=== SUNO STYLE PROMPT (paste into "Style of Music" field) ===
<ఒక English sentence — genre, vocals, "Telugu vocals", tempo, instruments, mood>

=== LYRICS (paste into "Lyrics" field) ===
[Chorus]
<పల్లవి — 4 lines, title hook, vocative తో start>

[Verse 1]
<చరణం 1 — 4–6 lines>

[Chorus]
<పల్లవి repeat>

...

[End]
```

Suno లో రెండు blocks ను respective fields లో paste చేయండి.

---

## 6. ముఖ్య conventions (గుర్తుంచుకోండి)

- **Lyrics ఎల్లప్పుడూ తెలుగు script లోనే** — transliteration (Roman) ఎప్పుడూ వద్దు.
- **Songs `[Chorus]` తో start అవుతాయి, `[Verse 1]` తో కాదు** — ఇది తెలుగు **పల్లవి-చరణం** సంప్రదాయం. మొదటి line లో song title hook ఉండాలి.
- **Suno tags మాత్రమే** — `[Verse N]`, `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[End]`. `[Intro]`, `[Outro]` ఎప్పుడూ వద్దు.
- **Lyrics block లో musical directions వద్దు** — `(soft piano)`, `(tabla fill)` లాంటివి style prompt block లో మాత్రమే.
- **Repetition shorthand వద్దు** — `(2)`, `(3)`, `||హుక్||` Suno చదవలేదు. Repeat కావాలంటే full గా రాయండి.
- **Generated `.txt` files always go into `created songs/`** — project root లో రాయడం వద్దు.
- **Agents `git commit / push / add` run చేయవు** — user explicit గా అడిగితే తప్ప.

---

## 7. ఎక్కడ ఏం దొరుకుతుంది (Quick reference)

| ఏం కావాలి | ఎక్కడ |
|-----------|------|
| పాటల project rules | [CLAUDE.md](CLAUDE.md) |
| Agent registry & pipelines | [.claude/agents/AGENTS.md](.claude/agents/AGENTS.md) |
| Song-writer skill (full details) | [.claude/skills/telugu-christian-song-writer/SKILL.md](.claude/skills/telugu-christian-song-writer/SKILL.md) |
| 100 Suno style prompts | [styles/INDEX.md](styles/INDEX.md) |
| Music-director style variants | [south indian telugu styles/](south%20indian%20telugu%20styles/) |
| Generated songs (working set) | [created songs/](created%20songs/) |
| Tested & approved songs | [tested/](tested/) |
| Orchestration log | [WORK-SUMMARY.md](WORK-SUMMARY.md) |

---

## 8. Typical workflow (సాధారణంగా ఇలా run చేస్తాను)

1. `/write-song-quick Christmas — Bethlehem and the manger` — fast గా ఒక Christmas song generate.
2. Output file open చేసి, రెండు blocks Suno లో paste చేసి generate చేయండి.
3. Suno output నచ్చకపోతే: `/review-songs created songs/<file>` — agent flag చేస్తే improved version use చేయండి.
4. Final song నచ్చితే: file ను `created songs/` నుంచి `tested/` లోకి move చేయండి.

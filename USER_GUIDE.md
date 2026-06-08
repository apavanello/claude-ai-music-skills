# Bitwize Music Plugin — Complete Workflow Guide

This guide walks you through the entire end-to-end music production process using the **53 skills** and **MCP tools** integrated into Hermes Agent.

```
                  ┌───────────────────────────────┐
                  │  1. IDEATION & PLANNING       │
                  │  (ideas -> concept -> album)  │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │  2. RESEARCH & VERIFICATION   │
                  │  (source gathering & audits)  │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │  3. SONGWRITING & LYRICS      │
                  │  (writing, refines, prosody)  │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │  4. QUALITY CONTROL GATES     │
                  │  (plagiarism, pronunciation)  │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │  5. SUNO GENERATION           │
                  │  (style prompt engineering)   │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │  6. MIXING & MASTERING        │
                  │  (polishing, loudness bounds) │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │  7. VISUALS & MARKETING       │
                  │  (artwork, promo videos)      │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │  8. DISTRIBUTION & RELEASE    │
                  │  (metadata, sheet music, QA)  │
                  └───────────────────────────────┘
```

---

## Phase 1: Setup & Session Start

Before starting, launch a fresh Hermes session and trigger the initialization.

```bash
hermes
```

In your chat session:
- **Initialize the environment:**
  > *"Run the `session-start` skill"*
  
  This verifies your plugin's environment paths, checks your virtual environment package health (`check_venv_health` tool), and loads the workspace settings.

---

## Phase 2: Album Ideation & Concept

### 1. Manage Ideas
If you don't have a concrete concept yet, brainstorm in your backlog:
- **Add a raw idea:**
  > *"Use `album-ideas` to add an album idea for a cyberpunk-themed synthwave EP"*
- **Refine ideas:**
  > *"Use `album-ideas` to list all pending ideas"*

### 2. Launch the Album
Once you select an idea (e.g., "Neon Dreams"), promote it to a project directory:
- **Promote an idea:**
  > *"Use the `promote-idea` skill to promote 'Neon Dreams'"*
  
  *(Alternatively, if creating a completely fresh album from scratch without using the ideas file, run: "Use the `new-album` skill to create 'Neon Dreams'".)*

### 3. Establish the Concept
Hermes will now trigger the `album-conceptualizer` skill to walk you through a 7-phase structural planning interview covering:
1. **Thematic core** (What is the story?)
2. **Sonic boundaries** (Instruments, tempos, soundscapes)
3. **Tracklist architecture** (Narrative arc, key/tempo progression)
4. **Target references** (Reference songs, artists, production styles)

---

## Phase 3: Research & Fact-Verification (Optional)

If you are creating an album based on real events, historical timelines, or documentary investigations:
- **Run the main researcher:**
  > *"Use the `researcher` skill to find details on the history of visual kei"*
- **Target specific sources:**
  - `researchers-legal` (court documents, filings)
  - `researchers-gov` (DOJ/SEC releases)
  - `researchers-financial` (filings, markets)
  - `researchers-biographical` (bios, interviews)
  - `researchers-tech` (changelogs, dev docs)
- **Review and verify sources:**
  > *"Use the `researchers-verifier` skill on the track list to validate all citations"*
  
  Once confirmed, lock the verification:
  > *"Use `verify-sources` to mark 'Track 1' as verified"*

---

## Phase 4: Songwriting & Lyric Crafting

Write and structure the lyrics for your tracks.

- **Create a track file:**
  > *"Create track 1 in 'Neon Dreams'"* (Hermes will use the track template to generate `01-neon-dreams.md` under `{content_root}/.../tracks/`).
- **Write lyrics:**
  > *"Use `lyric-writer` to write lyrics for track 1 about escaping a neon city"*
  
  This formats the lyrics with standard section headers like `[Verse]`, `[Chorus]`, `[Bridge]`.
- **Refine and tighten:**
  > *"Use `lyric-refiner` to do a multi-pass polish of the lyrics for track 1"*
  
  This adjusts syllable flow, tightens rhythms, resolves clichés, and aligns style patterns across all tracks.

---

## Phase 5: Quality Control (QC Gates)

Before generating any music, you must run your lyrics through 6 mandatory quality gates:

1. **Lyric Reviewer:**
   > *"Run the `lyric-reviewer` skill on track 1"*
   
   Audits the lyrics against a 14-point checklist (prosody, structural tags, rhyme schemes).
2. **Pronunciation Specialist:**
   > *"Run the `pronunciation-specialist` skill on track 1"*
   
   Scans the text for homographs or proper nouns that Suno might mispronounce and prompts you to add Phonetic Pronunciation Notes.
3. **Explicit Checker:**
   > *"Run the `explicit-checker` skill on the album"*
   
   Checks for profanity and verifies that explicit content tags are correct.
4. **Plagiarism Checker:**
   > *"Run the `plagiarism-checker` skill on track 1"*
   
   Scans search engines to verify your lines are distinct and do not accidentally copy existing songs.
5. **Voice Checker:**
   > *"Run the `voice-checker` skill on track 1"*
   
   Flags overly structured or abstract phrases that sound like standard AI defaults, keeping the lyrics unique.
6. **Final Gate Check:**
   > *"Run the `pre-generation-check` skill on track 1"*
   
   Verifies that all prior gates (1-5) have passed.

---

## Phase 6: Suno Audio Generation

Once the lyrics are fully cleared:

- **Construct Suno prompts:**
  > *"Use the `suno-engineer` skill to design Suno prompts for track 1"*
  
  This will create optimized **Style Prompts** and **Lyric Box Content** compliant with Suno V5 limits.
- **Copy to Clipboard:**
  > *"Use the `clipboard` skill to copy style prompts and lyrics for track 1"*
  
  Paste these directly into Suno to generate your song.
- **Import Audio:**
  Download the generated WAV file(s) from Suno. Move them to your local project directory:
  > *"Use the `import-audio` skill to save the downloaded WAV files into the album folder"*

---

## Phase 7: Audio Production (Mixing & Mastering)

Polish and master your raw audio to match professional streaming targets (-14 LUFS, -1.0 dBTP).

- **Audio Cleanup and Mix Polish:**
  > *"Use the `mix-engineer` skill to analyze and polish the mix for track 1"*
- **Mastering:**
  > *"Use the `mastering-engineer` skill to master track 1"*
  
  This runs the Python mastering pipeline (`master_tracks.py`), normalizing loudness, removing noise, adjusting balance, and creating dynamic range checks.
- **Verification:**
  > *"Run the `mono-fold-check` skill to test mono compatibility"*

---

## Phase 8: Visuals & Marketing

- **Create Artwork Concept:**
  > *"Use the `album-art-director` skill to create artwork prompts for the album"*
- **Import Album Art:**
  Save your generated cover image to your workspace:
  > *"Use `import-art` to save the cover image"*
- **Write Promo Copy:**
  > *"Use the `promo-writer` skill to generate social media posts for TikTok, Instagram, and X"*
- **Create Waveform Videos:**
  > *"Use the `promo-director` skill to generate 15-second vertical promo videos from the mastered audio"*
- **Upload Assets:**
  > *"Use the `cloud-uploader` skill to upload promo videos to Cloudflare R2 / AWS S3"*

---

## Phase 9: Sheet Music & Distribution

- **Sheet Music Generation:**
  > *"Use the `sheet-music-publisher` skill to convert mastered audio to PDF sheet music and assemble the album songbook"*
- **Release Coordination:**
  > *"Use the `release-director` skill to run final release QA checks"*
  
  This checks tags, artwork sizes, and formats, and builds your metadata distribution sheets.
- **Structural Integrity:**
  > *"Run the `validate-album` skill to make sure all files are in the right folder"*

---

## Utility Skills (Use Anytime)

- **Next Steps:**
  > *"Run the `next-step` skill"* - Evaluates the current state of your album and tells you the exact next task to complete.
- **Visual Dashboard:**
  > *"Run the `album-dashboard` skill"* - Displays a visual breakdown of your album's completion percentage per phase and lists blockers.
- **Status Summary:**
  > *"Run the `resume` skill <album-name>"* - Locates an album and shows its status, track list, and next actions.
- **Rename Project/Tracks:**
  > *"Run the `rename` skill to change track 1's title"* - Safely renames files, directories, and updates all internally tracked titles.
- **Interactive Tutorial:**
  > *"Run the `tutorial` skill"* - Starts an interactive walkthrough for users.
- **Help Menu:**
  > *"Run the `help` skill"* - Lists all skills and categories.
- **Run Tests:**
  > *"Run the `test` skill"* - Executes the plugin unit tests to ensure all python servers and paths are operating correctly.

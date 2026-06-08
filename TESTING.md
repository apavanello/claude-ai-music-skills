# Testing Plan for bitwize-music-plugin on Hermes Agent

Comprehensive testing checklist for the Bitwize Music plugin on Hermes Agent.

---

## Prerequisites

- Hermes Agent installed (`hermes` command available)
- Python 3.8+ installed
- Git configured
- A test directory outside the plugin repo (e.g., `~/test-music-plugin/`)

---

## Phase 1: Installation Testing

### 1.1 Fresh Install (Skills & MCP)

Follow the standard installation steps to link skills and add the MCP server:

```bash
# Link the skills to Hermes
mkdir -p ~/.hermes/skills/music
ln -sf "$(pwd)/skills/"* ~/.hermes/skills/music/

# Create venv and install requirements
uv venv ~/.bitwize-music/venv
uv pip install --python ~/.bitwize-music/venv -r requirements.txt
~/.bitwize-music/venv/bin/playwright install chromium

# Register MCP server
hermes mcp add bitwize-music-mcp \
  --command ~/.bitwize-music/venv/bin/python \
  --args "$(pwd)/servers/bitwize-music-server/run.py"
```

**Verify:**
- [ ] Hermes MCP registration completes successfully
- [ ] Run `hermes skills list` and verify all 53 `bitwize-music` skills are listed and marked as `enabled` under the `music` category.

---

## Phase 2: Configuration Testing

### 2.1 Initial Config Setup

```bash
# Copy example config
mkdir -p ~/.bitwize-music
cp config/config.example.yaml ~/.bitwize-music/config.yaml
```

Edit `~/.bitwize-music/config.yaml`:
```yaml
artist:
  name: "test-artist"

paths:
  content_root: "~/test-music-plugin/content"
  audio_root: "~/test-music-plugin/audio"
  documents_root: "~/test-music-plugin/documents"
  tools_root: "~/.bitwize-music"
  plugin_root: "."

urls:
  soundcloud: "https://soundcloud.com/test"

generation:
  service: suno
```

Create test directories:
```bash
mkdir -p ~/test-music-plugin/content/artists
mkdir -p ~/test-music-plugin/audio
mkdir -p ~/test-music-plugin/documents
```

**Verify:**
- [ ] No path-resolution errors on startup
- [ ] Path directories exist

---

## Phase 3: Core Workflow Testing

### 3.1 Tutorial & Resume Skills

Start a Hermes session:
```bash
hermes
```

In the session, prompt the agent:
`Use the tutorial skill to show help.`

**Verify:**
- [ ] Help message displays correctly, detailing `new-album`, `resume`, and `help`.

Next, prompt:
`Use the resume skill to check my albums.`

**Verify:**
- [ ] Scans `content_root` and reports no albums found (expected for clean install).

### 3.2 Album Creation

Prompt:
`Use the new-album skill to create a new album.`

Use these test details when prompted:
- Artist: "Test Artist"
- Genre: "electronic"
- Album name: "Test Album"
- Type: "Thematic"

**Verify:**
- [ ] Directory created: `{content_root}/artists/test-artist/albums/electronic/test-album/`
- [ ] Album `README.md` and `tracks/` subdirectory created successfully.

### 3.3 Lyric Writing and Review

Prompt:
`Use the lyric-writer skill to create 01-test-track.md and write a short electronic verse.`

**Verify:**
- [ ] File `01-test-track.md` is created in the `tracks/` directory.
- [ ] Lyrics are written with standard section tags (e.g. `[Verse]`).
- [ ] The automatic quality checklist runs (prosody, rhyme scheme).

---

## Phase 4: QC Gates & Verification

Verify that the verification and safety skills run properly:

1. **Pronunciation Specialist:**
   `Run the pronunciation-specialist skill on 01-test-track.md`
   - [ ] Scans for pronunciation risks and reports any homographs or issues.

2. **Explicit Checker:**
   `Run the explicit-checker skill on the Test Album`
   - [ ] Scans all album tracks and confirms explicit/clean status.

3. **Pre-generation Gates:**
   `Run the pre-generation-check skill on 01-test-track.md`
   - [ ] Verifies the 6 validation gates and reports readiness for generation.

---

## Phase 5: Git Safety Testing

Ensure that binary and source files are not tracked in git within the content area.

```bash
cd ~/test-music-plugin/content
git init
touch artists/test-artist/test.pdf
mkdir -p artists/test-artist/albums/electronic/test-album/primary-sources
touch artists/test-artist/albums/electronic/test-album/primary-sources/doc.pdf

git add .
git status
```

**Verify:**
- [ ] Both the `test.pdf` and the `primary-sources/` directory are NOT staged (correctly blocked by `.gitignore`).

---

## Phase 6: Cleanup

After testing:

```bash
# Remove test directories
rm -rf ~/test-music-plugin

# Remove MCP server from Hermes
hermes mcp remove bitwize-music-mcp

# Remove linked skills
rm -rf ~/.hermes/skills/music
```

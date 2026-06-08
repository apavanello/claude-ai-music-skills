# Bitwize Music Plugin — Hermes/Antigravity IDE

AI music generation workflow for [Suno](https://suno.com). This plugin provides 53 skills that turn a conversation into a full album production pipeline — from concept development to release.

> [!NOTE]
> This is a Hermes plugin port of the [claude-ai-music-skills](https://github.com/bitwize-music-studio/claude-ai-music-skills) project. Original license: CC0 (Public Domain).

---

## Install

This plugin is installed at `~/.gemini/config/plugins/bitwize-music-plugin/`.

### MCP Server Setup


The plugin includes an MCP server with 80+ tools for state queries, audio analysis, lyrics processing, and database operations. To enable it, add the following to your MCP configuration:

```json
{
  "mcpServers": {
    "bitwize-music-mcp": {
      "type": "stdio",
      "command": "${HOME}/.bitwize-music/venv/bin/python3",
      "args": ["${HOME}/.gemini/config/plugins/bitwize-music-plugin/servers/bitwize-music-server/run.py"]
    }
  }
}
```

### Python Dependencies

```bash
# Create unified venv
python3 -m venv ~/.bitwize-music/venv

# Install ALL plugin dependencies
~/.bitwize-music/venv/bin/pip install -r ~/.gemini/config/plugins/bitwize-music-plugin/servers/bitwize-music-server/../../requirements.txt

# Set up document hunter browser (optional)
~/.bitwize-music/venv/bin/playwright install chromium
```

### First-Time Configuration

```bash
cp ~/.gemini/config/plugins/bitwize-music-plugin/config/config.example.yaml ~/.bitwize-music/config.yaml
```

Edit `~/.bitwize-music/config.yaml` to set your artist name and workspace paths.

---

## Skills (53)

Skills are automatically activated by the AI agent based on context. Each skill contains domain expertise for a specific part of the music production workflow.

### Album & Track Creation
| Skill | Description |
|-------|-------------|
| `album-ideas` | Track and manage album ideas |
| `promote-idea` | Convert a Pending idea into a full album |
| `new-album` | Create new album with directory structure |
| `album-conceptualizer` | Album concepts and tracklist architecture |
| `lyric-writer` | Write/review lyrics with professional prosody and rhyme craft |
| `suno-engineer` | Technical Suno V5/V5.5 prompting and genre selection |

### Research & Sources
| Skill | Description |
|-------|-------------|
| `researcher` | Main research coordinator, fact-checking |
| `document-hunter` | Automated document search/download |
| `researchers-legal` | Court documents, indictments |
| `researchers-gov` | DOJ/FBI/SEC releases |
| `researchers-tech` | Project histories, changelogs |
| `researchers-journalism` | Investigative articles |
| `researchers-security` | Malware analysis, CVEs |
| `researchers-financial` | SEC filings, market data |
| `researchers-historical` | Archives, timelines |
| `researchers-biographical` | Personal backgrounds |
| `researchers-primary-source` | Tweets, blogs, forums |
| `researchers-verifier` | Quality control, citation validation |

### Quality Control
| Skill | Description |
|-------|-------------|
| `lyric-reviewer` | Pre-generation QC gate (14-point checklist) |
| `lyric-refiner` | Post-writing multi-pass refinement |
| `pronunciation-specialist` | Scan for pronunciation risks |
| `explicit-checker` | Verify explicit content flags |
| `plagiarism-checker` | Check lyrics for phrases matching existing songs |
| `voice-checker` | Detect AI-written patterns in lyrics and prose |
| `pre-generation-check` | Final pre-generation checkpoint (6 gates) |
| `validate-album` | Validate album structure and paths |

### Production & Release
| Skill | Description |
|-------|-------------|
| `album-art-director` | Visual concepts and AI art prompts |
| `mix-engineer` | Audio polishing, fixing Suno artifacts |
| `mastering-engineer` | Audio mastering guidance |
| `promo-director` | Generate promo videos for social media |
| `promo-writer` | Platform-specific social media copy |
| `promo-reviewer` | Review and quality-check promo content |
| `cloud-uploader` | Upload promo videos to Cloudflare R2 or AWS S3 |
| `sheet-music-publisher` | Convert audio to sheet music |
| `release-director` | Release coordination and distribution |

### File Management & Workflow
| Skill | Description |
|-------|-------------|
| `import-track` | Move track .md files to album location |
| `import-audio` | Move audio files to album location |
| `import-art` | Place album art in correct locations |
| `clipboard` | Copy track lyrics/prompts to clipboard |
| `rename` | Rename albums or tracks |
| `session-start` | Run session startup procedure |
| `resume` | Find an album and show status with next steps |
| `next-step` | Get recommended next action |
| `album-dashboard` | Visual album progress dashboard |

### System & Maintenance
| Skill | Description |
|-------|-------------|
| `setup` | Detect environment and install dependencies |
| `configure` | Edit plugin configuration |
| `health-check` | Plugin health checks |
| `test` | Run automated tests |
| `tutorial` | Interactive guided album creation |
| `genre-creator` | Create new genre directories |
| `verify-sources` | Human source verification gate |
| `help` | Show available skills and workflows |
| `about` | About bitwize and this plugin |

---

## Workflow Overview

```
Concept → Research → Write (+Suno Prompt) → [Refine] → QC/Verify → Generate → [Polish] → Master → Promo Videos → Release
```

**Key rules:**
- Research must complete before writing for source-based content
- Human source verification is required before generation
- Audio must be polished before mastering

---

## Configuration & Path Resolution

Config is at: `~/.bitwize-music/config.yaml`

**Path variables** (from config):
- `{content_root}` = `paths.content_root`
- `{audio_root}` = `paths.audio_root`
- `{documents_root}` = `paths.documents_root`
- `{tools_root}` = `~/.bitwize-music`
- `[artist]` = `artist.name`

**Mirrored path structure:**
```
{content_root}/artists/[artist]/albums/[genre]/[album]/   # Album files (in git)
{audio_root}/artists/[artist]/albums/[genre]/[album]/     # Mastered audio
{documents_root}/artists/[artist]/albums/[genre]/[album]/ # PDFs (not in git)
```

---

## Core Principles

**Be a collaborator, not a yes-man.** Push back when ideas don't work. The goal is good music, not agreement.

**Preserve exact casing and spelling.** "bitwize" stays "bitwize" — never auto-capitalize user-provided names.

**Ask when unsure.** Word choice, style, structure, Suno settings — don't guess.

**Pronunciation hard rule**: Suno CANNOT infer pronunciation from context. When any homograph is found, **ASK** the user which pronunciation is intended.

---

## Genre Coverage

72 genre directories with production guides, mastering presets, artist deep-dives, and Suno-specific tips. Located in `genres/` within the plugin directory.

---

## License

CC0 — Public Domain. Do whatever you want with it.

## Disclaimer

Artist and song references in the genre documentation are for educational and reference purposes only. This plugin does not encourage creating infringing content.

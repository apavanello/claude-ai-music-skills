# Installing on Hermes Agent

This project (`claude-ai-music-skills`) is designed as a hybrid integration for [Hermes Agent by Nous Research](https://github.com/NousResearch/hermes-agent). It combines **Markdown Skills** for natural language workflows and an **MCP Server** for Python-based tool execution.

Because it uses this hybrid approach, you should **NOT** use `hermes plugins install` (which expects a native Python plugin format with `plugin.yaml`). Instead, follow these steps to manually link the skills and register the MCP server.

## 1. Link the Skills

Hermes Agent auto-discovers Markdown skills in `~/.hermes/skills/`. Link the skills directory from this repository:

```bash
mkdir -p ~/.hermes/skills/music
# Assuming you cloned the repo to ~/Projects/claude-ai-music-skills
ln -s ~/Projects/claude-ai-music-skills/skills/* ~/.hermes/skills/music/
```

## 2. Set Up the Python Environment

The MCP server requires Python dependencies. Create a virtual environment and install the requirements using `uv` (recommended):

```bash
uv venv ~/.bitwize-music/venv
uv pip install --python ~/.bitwize-music/venv -r ~/Projects/claude-ai-music-skills/requirements.txt
```

## 3. Configure the MCP Server

Add the MCP server to Hermes Agent so the skills can access its 80+ tools.

```bash
hermes mcp add bitwize-music-mcp \
  --command ~/.bitwize-music/venv/bin/python \
  --args ~/Projects/claude-ai-music-skills/servers/bitwize-music-server/run.py
```
*(When prompted, type `Y` to enable all tools)*

## 4. Verification

Restart Hermes Agent and list your skills to verify the installation:

```bash
hermes skills list
```
You should see all 53 `bitwize-music` skills enabled under the `music` category. You can now use them directly in your Hermes Agent chats!

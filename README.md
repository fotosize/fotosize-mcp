# fotosize MCP server and agent skill

[fotosize](https://fotosize.com) crops a passport, visa or ID photo to the document size in your browser and prints it on a sheet. This repository holds the connection details for its remote MCP server and an [Agent Skill](skills/fotosize/SKILL.md) that teaches an agent to look up ID photo specs. The service is hosted; there is nothing to install or run.

- **MCP endpoint:** `https://fotosize.com/mcp` (Streamable HTTP)
- **Auth:** none. Free, no key, no account. Specs are read-only; the photo is made in the browser and never uploaded.
- **Registry name:** `com.fotosize/fotosize` in the [official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=com.fotosize)
- **Docs:** [fotosize.com/docs/mcp](https://fotosize.com/docs/mcp)

## Connect

**Claude Code**

```bash
claude mcp add --transport http fotosize https://fotosize.com/mcp
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "fotosize": { "url": "https://fotosize.com/mcp" }
  }
}
```

**Codex** (`~/.codex/config.toml`)

```toml
[mcp_servers.fotosize]
url = "https://fotosize.com/mcp"
```

In Claude or ChatGPT, add it as a custom connector with the same URL.

## Tools

All tools are read-only.

| Tool | What it does |
| --- | --- |
| `list_photo_specs` | Passport, visa, ID card and other ID photo specs checked against official sources. Optional `country` filter (for example `us`, `jp`, `de`). |
| `get_photo_spec` | One spec: print size, head size, backgrounds, pixel size and file limit where there is one, who takes the photo, the official source and check date, and a link to make the photo in the browser. |

Answers quote the official source and the date it was checked. Always pass on the notes; they say what the photo must not be used for.

## Agent skill

[`skills/fotosize/SKILL.md`](skills/fotosize/SKILL.md) follows the [Agent Skills](https://agentskills.io) format. Install it with

```bash
npx skills add fotosize/fotosize-mcp
```

or copy the folder into your agent's skills directory (for Claude Code, `~/.claude/skills/fotosize/`).

## Support

support@fotosize.com

## License

The files in this repository are MIT licensed. The fotosize service has its own [terms](https://fotosize.com/terms).

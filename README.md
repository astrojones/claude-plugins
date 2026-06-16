# claude-plugins

The **astrojones** Claude Code plugin marketplace — just the index, nothing else.
Each plugin lives in its own repo; this repo exists so no plugin repo has to
double as a marketplace.

## Use

```bash
claude plugin marketplace add astrojones/claude-plugins
claude plugin install astrojones@astrojones    # repo agent harness + coding workflows
claude plugin install deploy@astrojones   # astrojones org deploy layer (requires astrojones)
```

## What's listed

| Plugin | Repo | What it is |
|--------|------|------------|
| `astrojones` | [astrojones/astrojones](https://github.com/astrojones/astrojones) | The repo agent harness as a Claude Code plugin: a bundled, auto-connecting MCP server (`repo_*` tools + proxied `serena_*` code navigation), safety hooks, and generic coding-workflow skills and subagents. Harnesses any repo automatically on connect (`AGENTS.md` is opt-out). Generic — not tied to any one org. |
| `deploy` | [astrojones/deploy](https://github.com/astrojones/deploy) | The astrojones org deploy layer: nuklaut deploy knowledge, `/new-app` + `/harness-app` scaffolding, deploy-doctor CI diagnosis, the scaffold templates, and pyproject-canon. Org-internal/private. Requires the `astrojones` plugin. |

## How duplication is avoided

`astrojones` ships its harness MCP server bundled in the plugin, and it
auto-connects in Claude Code — no per-repo `.mcp.json` setup needed there.

For CI or other non-Claude-Code clients, `astrojones`'s `repo_bootstrap(pin="<sha>")`
materializes a project-pinned `.mcp.json` entry instead, so the same server can
run outside Claude Code without drifting from the plugin version.

`deploy` is the org layer on top and ships **no server of its own** — `/new-app`
and `/harness-app` call `astrojones`'s `repo_bootstrap` MCP tool for harness setup.
So installing both plugins never runs duplicate servers: there's exactly one
harness server, either bundled-and-auto-connected (Claude Code) or
sha-pinned-in-`.mcp.json` (everywhere else).

## Maintenance

Plugin releases happen in the individual plugin repos (bump their `plugin.json`).
Touch this repo only to add/remove a plugin or change its index metadata.

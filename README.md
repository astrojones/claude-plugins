# claude-plugins

The **astrojones** Claude Code plugin marketplace — just the index, nothing else.
Each plugin lives in its own repo; this repo exists so no plugin repo has to
double as a marketplace.

## Use

```bash
claude plugin marketplace add astrojones/claude-plugins
claude plugin install astrojones-dev@astrojones        # the one org plugin
```

## What's listed

| Plugin | Repo | What it is |
|--------|------|------------|
| `astrojones-dev` | [astrojones/astrojones-dev](https://github.com/astrojones/astrojones-dev) | The org plugin: nuklaut deploy knowledge, `/new-app` scaffolding, deploy-doctor CI diagnosis, plus the repo-agent-harness Claude Code surface (workflow skills, subagents, safety-hook shims, `/harness-init`). |

[`repo-agent-harness`](https://github.com/astrojones/repo-agent-harness) itself is **not a
plugin** — it's the per-repo MCP server + scaffolder, installed into each repo as a
sha-pinned `.mcp.json` entry.

## The two-layer rule (why nothing is duplicated)

- **Per repo:** `/new-app` (or `repo-agent-harness init`) scaffolds each app with its own
  sha-pinned harness **MCP server** in `.mcp.json` — works with any MCP-capable assistant,
  no plugins needed.
- **Per user:** the plugin above adds Claude Code **workflows** (skills, agents, hooks,
  commands). It ships **no MCP server**.

So installing the plugin *and* working in scaffolded repos never runs duplicate servers:
the server always comes from the repo, the workflows from the plugin.

## Maintenance

Plugin releases happen in the plugin repos (bump their `plugin.json`). Touch this repo
only to add/remove a plugin or change its index metadata.

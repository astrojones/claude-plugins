# claude-plugins

The **astrojones** Claude Code plugin marketplace — just the index, nothing else.
Each plugin lives in its own repo; this repo exists so no plugin repo has to
double as a marketplace.

## Use

```bash
claude plugin marketplace add astrojones/claude-plugins
claude plugin install astrojones-dev@astrojones        # org deploy/scaffold toolkit
claude plugin install repo-agent-harness@astrojones    # coding-workflow skills + /init
```

## What's listed

| Plugin | Repo | What it is |
|--------|------|------------|
| `astrojones-dev` | [astrojones/astrojones-dev](https://github.com/astrojones/astrojones-dev) | nuklaut deploy knowledge, `/new-app` scaffolding, deploy-doctor CI diagnosis. |
| `repo-agent-harness` | [astrojones/repo-agent-harness](https://github.com/astrojones/repo-agent-harness) | Coding-workflow skills, subagents, safety hooks, `/repo-agent-harness:init`. |

## The two-layer rule (why nothing is duplicated)

- **Per repo:** `/new-app` (or `repo-agent-harness init`) scaffolds each app with its own
  sha-pinned harness **MCP server** in `.mcp.json` — works with any MCP-capable assistant,
  no plugins needed.
- **Per user:** the plugins above add Claude Code **workflows** (skills, agents, hooks,
  commands). They ship **no MCP server**.

So installing the plugins *and* working in scaffolded repos never runs duplicate servers:
the server always comes from the repo, the workflows from the plugins.

## Maintenance

Plugin releases happen in the plugin repos (bump their `plugin.json`). Touch this repo
only to add/remove a plugin or change its index metadata.

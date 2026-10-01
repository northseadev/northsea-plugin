# Northsea plugin for Claude Code

Connects Claude Code to [Northsea](https://northsea.co) through the Northsea MCP
server, so you can ask about your studies and their results in plain language:
"which of our studies are in fieldwork?", "what did respondents in the UK
segment say about pricing?", "what is the NPS for the March wave?".

The plugin contains no code. It tells Claude Code where the server is
(`https://mcp.northsea.co/mcp`), and you sign in with your own Northsea account.
Claude then sees exactly what you can see in the Northsea app, and nothing more.

## Install

You need Claude Code and a Northsea account.

In a Claude Code session:

```
/plugin marketplace add northseadev/northsea-plugin
/plugin install northsea@northsea
/reload-plugins
```

Or from your shell:

```bash
claude plugin marketplace add northseadev/northsea-plugin
claude plugin install northsea@northsea
```

## Sign in

The first time, connect your Northsea account:

1. In Claude Code, run `/mcp`.
2. Select `plugin:northsea:northsea` and choose **Authenticate**.
3. Your browser opens. Sign in to Northsea and approve the connection.

From your shell, `claude mcp login plugin:northsea:northsea` does the same.

To check it worked, run `claude mcp list`: `plugin:northsea:northsea` should
show as connected rather than "Needs authentication".

## What Claude can do with it

| Tool              | What it does                                                                                                                                |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `list_my_studies` | Lists the studies your account can see in an organization, with their status and when they went live.                                      |
| `get_study`       | One study in full: status, audience segments and markets, the questionnaire, and the AI executive summary from the Results page.            |
| `query_findings`  | Results per question, computed the same way as the Results page: answer distributions, NPS, means, and the written answers to open questions. |

Every tool is read-only. The server checks your Northsea permissions on every
call, so Claude only sees the studies and results your account can see in the
app.

## Updating

```bash
claude plugin marketplace update northsea
claude plugin update northsea@northsea
```

Or turn on auto-update for the `northsea` marketplace under **Marketplaces** in
`/plugin`.

## Disconnecting

- Sign out: `claude mcp logout plugin:northsea:northsea`.
- Remove the plugin: `claude plugin uninstall northsea@northsea`.

## Other agents

This repository is also an [Agent Plugins 1.0](https://agent-plugins.org)
package: `plugin.json` and `mcp.json` at the root. Agents that support that
standard can load it as a plugin; see your agent's documentation for adding a
plugin from a git repository.

| File                              | Read by                 |
| --------------------------------- | ----------------------- |
| `plugin.json`                     | Agent Plugins clients   |
| `mcp.json`                        | Both                    |
| `.claude-plugin/plugin.json`      | Claude Code             |
| `.claude-plugin/marketplace.json` | Claude Code marketplace |

The same server also works without any plugin. Use the URL
`https://mcp.northsea.co/mcp`:

- **Claude (web and desktop):** Settings, Connectors, Add custom connector.
  Paste the URL, then sign in to Northsea.
- **ChatGPT:** Settings, Apps & Connectors, Advanced settings. Turn on
  Developer mode, then Create. Paste the URL, choose OAuth, then sign in to
  Northsea.
- **Claude Code without the plugin:**
  `claude mcp add --transport http northsea https://mcp.northsea.co/mcp`, then
  `/mcp` to sign in.

## Help

Questions or problems: open an issue on this repository, or contact your
Northsea account team.

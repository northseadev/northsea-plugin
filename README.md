# Northsea plugin

Connects your AI agent to [Northsea](https://northsea.co) through the Northsea
MCP server, so you can ask about your studies and their results in plain
language: "which of our studies are in fieldwork?", "what did respondents in
the UK segment say about pricing?", "what is the NPS for the March wave?".

## What's in this repository

The plugin is an [Agent Plugins 1.0](https://agent-plugins.org) package, with
client-specific files alongside it for agents that use their own format.

| Path                              | Purpose                                                                                   |
| --------------------------------- | ----------------------------------------------------------------------------------------- |
| `plugin.json`                     | Agent Plugins manifest. Also holds the OpenAI plugin directory listing under `extensions` |
| `mcp.json`                        | The Northsea MCP server, shared by every client                                           |
| `assets/`                         | Logos and icons for the OpenAI plugin directory listing                                   |
| `.claude-plugin/plugin.json`      | Claude Code plugin manifest, pointing at `mcp.json`                                       |
| `.claude-plugin/marketplace.json` | Lets Claude Code install the plugin from this repository                                  |

## Install

You need a Northsea account and an agent that supports Agent Plugins or MCP.

- **Agents that support Agent Plugins:** add this repository
  (`https://github.com/northseadev/northsea-plugin`) as a plugin. See your
  agent's documentation for how.
- **Claude Code:** see [Claude Code](#claude-code) below.
- **Any other MCP client:** add `https://mcp.northsea.co/mcp` as a remote
  (streamable HTTP) MCP server with OAuth.

## Sign in

The first time your agent connects, it asks you to authenticate the `northsea`
server. Your browser opens; sign in to Northsea and approve the connection.

## Claude Code

### Install

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

### Sign in

1. In Claude Code, run `/mcp`.
2. Select `plugin:northsea:northsea` and choose **Authenticate**.
3. Your browser opens. Sign in to Northsea and approve the connection.

From your shell, `claude mcp login plugin:northsea:northsea` does the same.

To check it worked, run `claude mcp list`: `plugin:northsea:northsea` should
show as connected rather than "Needs authentication".

### Updating

```bash
claude plugin marketplace update northsea
claude plugin update northsea@northsea
```

Or turn on auto-update for the `northsea` marketplace under **Marketplaces** in
`/plugin`.

### Disconnecting

- Sign out: `claude mcp logout plugin:northsea:northsea`.
- Remove the plugin: `claude plugin uninstall northsea@northsea`.

## Help

Questions or problems: open an issue on this repository, or contact your
Northsea account team.

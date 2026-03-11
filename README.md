# PlanetScale Plugin

Agent plugin that bundles the [PlanetScale MCP server](https://planetscale.com/docs/connect/mcp) and [Database Skills](https://db-skills.com/) for GitHub Copilot. Works with both **VS Code** and the **Copilot CLI**.

## What's included

**MCP Server** — Authenticated access to your PlanetScale organizations, databases, branches, schema, and Insights data. No local setup required.

**Database Skills** — Expert knowledge for MySQL, PostgreSQL, Vitess, and Postgres sharding (Neki), loaded on-demand into Copilot's context.

## Install

This plugin is being submitted to the [copilot-plugins](https://github.com/github/copilot-plugins) and [awesome-copilot](https://github.com/github/awesome-copilot) marketplaces. Once accepted, it will be discoverable via `@agentPlugins` in VS Code and `copilot plugin marketplace browse` in the CLI.

Until then, you can install it directly from this repo.

### Copilot CLI

```bash
copilot plugin install planetscale/vscode-plugin
```

See [Installing plugins](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-finding-installing) for more details.

### VS Code

1. Clone the repo:

   ```bash
   git clone https://github.com/planetscale/vscode-plugin.git
   ```

2. Register the plugin path in your VS Code settings (`Cmd+,` / `Ctrl+,`, search for `chat.plugins.paths`):

   ```jsonc
   // settings.json
   "chat.plugins.paths": {
     "/path/to/vscode-plugin": true
   }
   ```

3. Reload VS Code.

> Agent plugins require the `chat.plugins.enabled` setting to be enabled (on by default in VS Code 1.100+). See [Agent plugins in VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-plugins) for more details.

### Verify it loaded

- **Skills**: Open the Chat view and select the gear icon > **Configure Skills** — you should see `mysql`, `postgres`, `vitess`, and `neki` listed
- **MCP**: Check the MCP server list to confirm the `planetscale` server is connected

## Skills source and sync

Skills are sourced from the [planetscale/database-skills](https://github.com/planetscale/database-skills) repository. A copy lives in `skills/` for install compatibility, and a Git submodule at `database-skills/` tracks the upstream.

GitHub Actions runs `.github/workflows/update-skills.yml` weekly (with manual `workflow_dispatch` support). When the upstream has new commits, the workflow copies the latest skills into `skills/` and opens a PR.

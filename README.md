# PlanetScale VS Code Plugin

Agent plugin for installing the [PlanetScale MCP server](https://planetscale.com/docs/connect/mcp) and [Database Skills](https://db-skills.com/) into VS Code via GitHub Copilot.

## What's included

**MCP Server** — Authenticated access to your PlanetScale organizations, databases, branches, schema, and Insights data. No local setup required.

**Database Skills** — Expert knowledge for MySQL, PostgreSQL, Vitess, and Postgres sharding (Neki), loaded on-demand into Copilot's context.

## Install

> Agent plugins require VS Code with the `chat.plugins.enabled` setting enabled (on by default in VS Code 1.100+).

### From the GitHub repo

Using the [Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-finding-installing#install-directly-from-an-online-git-repository):

```bash
copilot plugin install planetscale/vscode-plugin
```

### From a local clone

1. Clone with submodules:

   ```bash
   git clone --recurse-submodules https://github.com/planetscale/vscode-plugin.git
   ```

2. Register the plugin in your VS Code settings (`Cmd+,` or `Ctrl+,`, then search for `chat.plugins.paths`):

   ```jsonc
   // settings.json
   "chat.plugins.paths": {
     "/path/to/vscode-plugin": true
   }
   ```

3. Reload VS Code.

### Verify it loaded

- Open the Chat view and select the gear icon > **Configure Skills** — you should see `mysql`, `postgres`, `vitess`, and `neki` listed
- Check the MCP server list to confirm the `planetscale` server is connected

## Skills source and sync

This plugin pulls in skills from the upstream `planetscale/database-skills` repository via a Git submodule.

- Source repo: `https://github.com/planetscale/database-skills`
- Submodule path: `database-skills`
- Tracked branch: `main`

### Local bootstrap

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```

### Manual one-off update

To pull the latest upstream skills:

```bash
git submodule sync --recursive
git submodule update --init --remote database-skills
```

Commit the resulting submodule pointer change.

### Automated weekly updates

GitHub Actions runs `.github/workflows/update-skills.yml` weekly and supports manual runs (`workflow_dispatch`). When `database-skills` has new commits, the workflow opens a PR with the submodule pointer update.

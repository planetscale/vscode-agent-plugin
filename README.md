# PlanetScale VS Code Plugin

Agent plugin for installing the [PlanetScale MCP server](https://planetscale.com/docs/connect/mcp) and [Database Skills](https://db-skills.com/) into VS Code via GitHub Copilot.

## What's included

**MCP Server** — Authenticated access to your PlanetScale organizations, databases, branches, schema, and Insights data. No local setup required.

**Database Skills** — Expert knowledge for MySQL, PostgreSQL, Vitess, and Postgres sharding (Neki), loaded on-demand into Copilot's context.

## Install from the plugin marketplace

1. Open the Extensions view (`Ctrl+Shift+X` / `Cmd+Shift+X`)
2. Enter `@agentPlugins` in the search field
3. Find **PlanetScale** and select **Install**

The plugin requires the `chat.plugins.enabled` setting to be enabled (it is by default in VS Code 1.100+).

### Verify it loaded

- Open the Chat view and type `/` — you should see `mysql`, `postgres`, `vitess`, and `neki` skills listed
- Check the MCP server list to confirm the `planetscale` server is connected

## Test locally

To test this plugin from a local checkout:

1. Clone with submodules:

   ```bash
   git clone --recurse-submodules https://github.com/planetscale/vscode-plugin.git
   ```

2. Add the plugin path to your VS Code settings:

   ```jsonc
   // settings.json
   "chat.plugins.paths": {
     "/path/to/vscode-plugin": true
   }
   ```

3. Reload VS Code. The skills and MCP server should appear in Copilot chat.

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

## Submitting to marketplaces

This plugin is submitted to two GitHub Copilot plugin marketplaces:

- **[github/copilot-plugins](https://github.com/github/copilot-plugins)** — The official GitHub Copilot plugins collection
- **[github/awesome-copilot](https://github.com/github/awesome-copilot)** — Community-contributed plugins and customizations

See `CONTRIBUTING-UPSTREAM.md` for the exact PR content for each.

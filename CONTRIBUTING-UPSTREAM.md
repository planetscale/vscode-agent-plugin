# Upstream Marketplace Submissions

This document contains the exact content needed for PRs to the two GitHub Copilot plugin marketplaces.

## 1. github/copilot-plugins

**Target branch:** `main`

Add the following entry to the `plugins` array in `.github/plugin/marketplace.json`:

```json
{
  "name": "planetscale",
  "source": {
    "source": "github",
    "repo": "planetscale/vscode-plugin"
  },
  "description": "PlanetScale database tools — query schemas, run SQL, get performance insights, and access expert database knowledge for MySQL, PostgreSQL, Vitess, and Postgres sharding.",
  "version": "1.0.0"
}
```

### PR description

```
## Add PlanetScale plugin

Adds the PlanetScale plugin as an external reference to `planetscale/vscode-plugin`.

### What it provides

- **MCP Server**: Authenticated access to PlanetScale organizations, databases, branches, schema, and query performance Insights via the hosted PlanetScale MCP endpoint
- **4 Database Skills**: MySQL, PostgreSQL, Vitess, and Neki (Postgres sharding) — expert knowledge loaded on-demand into Copilot context

### Source repository

https://github.com/planetscale/vscode-plugin
```

---

## 2. github/awesome-copilot

**Target branch:** `staged` (NOT main)

Add the following entry to `plugins/external.json`:

```json
{
  "name": "planetscale",
  "description": "PlanetScale database tools — MCP server for live database access plus expert skills for MySQL, PostgreSQL, Vitess, and Postgres sharding readiness.",
  "version": "1.0.0",
  "author": {
    "name": "PlanetScale",
    "url": "https://planetscale.com"
  },
  "homepage": "https://github.com/planetscale/vscode-plugin",
  "keywords": [
    "database",
    "mysql",
    "postgresql",
    "vitess",
    "schema",
    "sql",
    "performance",
    "planetscale"
  ],
  "license": "MIT",
  "repository": "https://github.com/planetscale/vscode-plugin",
  "source": {
    "source": "github",
    "repo": "planetscale/vscode-plugin"
  }
}
```

After adding to `external.json`, run `npm run build` to regenerate `marketplace.json`.

### PR description

```
## Add PlanetScale external plugin

Adds PlanetScale as an external plugin in `plugins/external.json`, pointing to `planetscale/vscode-plugin`.

### What it provides

- **MCP Server**: Authenticated access to PlanetScale databases via hosted MCP endpoint (no local setup)
- **4 Database Skills**:
  - `mysql` — Schema design, indexing, query tuning, transactions, and operations for MySQL/InnoDB
  - `postgres` — Best practices, query optimization, MVCC, connection pooling, and PlanetScale-specific Postgres tooling
  - `vitess` — VSchema, sharding, vindexes, online DDL, and VReplication for PlanetScale Vitess databases
  - `neki` — Sharding readiness for PostgreSQL (PlanetScale's sharded Postgres)

### Source repository

https://github.com/planetscale/vscode-plugin
```

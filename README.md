# Renovate Config — alexcarol

Shared [Renovate](https://docs.renovatebot.com/) configuration for all repositories in the `alexcarol` GitHub account.

This repository uses Renovate's [shareable config presets](https://docs.renovatebot.com/config-presets/) feature. Each repo includes a small `renovate.json` that extends this shared preset — keeping per-repo configs minimal.

## How It Works

Renovate looks for `default.json` in `<user>/renovate-config` when a repo extends `github>alexcarol/renovate-config`. The preset is applied as a baseline; any per-repo `renovate.json` rules are merged on top.

Each repo needs a `renovate.json` that extends this preset:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>alexcarol/renovate-config"]
}
```

## What's Included

| Rule | Description |
|------|-------------|
| `config:best-practices` | Renovate's recommended base configuration |
| `packages:stylelint` | Stylelint ecosystem awareness |
| Lock file maintenance | Periodic lock file refresh PRs |
| Cloudflare grouping | Groups `wrangler` updates into a single PR |
| Dev tooling automerge | Auto-merges minor/patch updates for ESLint, Stylelint, Karma, and Jasmine packages |

## Adding Repo-Specific Rules

Add extra rules on top of the preset in the repo's `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>alexcarol/renovate-config",
    "monorepo:react"
  ],
  "packageRules": [
    {
      "description": "Group Tailwind CSS packages",
      "matchPackageNames": ["tailwindcss", "@tailwindcss/**"],
      "groupName": "Tailwind CSS packages"
    }
  ]
}
```

The shared rules (Cloudflare grouping, dev tooling automerge, etc.) still apply.

## Official Documentation

- [Shareable Config Presets](https://docs.renovatebot.com/config-presets/) — how presets work
- [Config Presets for Organization](https://docs.renovatebot.com/config-presets/#organization-level-presets) — org-level presets

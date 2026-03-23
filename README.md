# Renovate Config — alexcarol

Shared [Renovate](https://docs.renovatebot.com/) configuration for all repositories in the `alexcarol` GitHub organization.

This repository uses Renovate's [inherited config](https://docs.renovatebot.com/config-presets/) feature so that **every org repo gets these defaults automatically** — no per-repo `renovate.json` needed.

## How It Works

Renovate looks for `org-inherited-config.json` in `<org>/renovate-config` before processing any repository. If found, it applies the configuration as a baseline to all repos where the Renovate app is installed.

**Requirements:**
- The Renovate GitHub App must be installed on this `renovate-config` repository
- The app must also be installed on any repo you want to receive updates

## What's Included

| Rule | Description |
|------|-------------|
| `config:best-practices` | Renovate's recommended base configuration |
| `packages:stylelint` | Stylelint ecosystem awareness |
| Lock file maintenance | Periodic lock file refresh PRs |
| Cloudflare grouping | Groups `wrangler` updates into a single PR |
| Dev tooling automerge | Auto-merges minor/patch updates for ESLint, Stylelint, Karma, and Jasmine packages |

## Overriding the Inherited Config

If a repo needs to **add rules on top of** the inherited config, create a `renovate.json` in that repo. Renovate merges per-repo config on top of inherited config:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "packageRules": [
    {
      "description": "Also automerge TypeScript minor/patch",
      "matchPackageNames": ["typescript"],
      "matchUpdateTypes": ["minor", "patch"],
      "automerge": true
    }
  ]
}
```

The inherited rules (Cloudflare grouping, dev tooling automerge, etc.) still apply — the per-repo config is additive.

## Starting from Scratch (Ignoring Inherited Config)

If a repo needs a **completely independent** Renovate configuration that ignores the org defaults, set `ignorePresets` in the repo's `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "ignorePresets": ["config:best-practices", "packages:stylelint"],
  "extends": ["config:recommended"],
  "packageRules": []
}
```

This tells Renovate to disregard the presets inherited from the org config. You then define everything from scratch in the per-repo file.

Alternatively, to fully opt out of Renovate for a specific repo, simply don't install the Renovate app on that repo.

## Official Documentation

- [Shareable Config Presets](https://docs.renovatebot.com/config-presets/) — how presets and inheritance work
- [Self-Hosted Configuration](https://docs.renovatebot.com/self-hosted-configuration/) — `inheritConfig`, `inheritConfigRepoName`, `inheritConfigFileName`
- [Mend Hosted Apps Config](https://docs.renovatebot.com/mend-hosted/hosted-apps-config/) — specifics for the hosted Renovate GitHub App

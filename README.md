# renovate-preset

Shared [Renovate](https://docs.renovatebot.com/) preset used across achimismaili projects.

## Usage

Add to any repository's `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>achimismaili/renovate-preset"]
}
```

The `github>` preset scheme works from both GitHub and Azure DevOps Renovate runs, so this preset can be consumed by any host.

## Policy summary

- **Automerged** (after CI passes): external `devDependency` patch updates only, on the release branch
- **Manual review required**: internal easy-web packages (`@easy-web/**` on the Azure DevOps instances, `@achimismaili/easy-web-*` on the GitHub-hosted portfolio), `turbo`, `@inlang/paraglide-js`, any minor update, any runtime dependency change
- **Never automerged**: major updates — one PR per package for review context

> Both easy-web scopes must stay listed in `default.json`. The same source repo
> publishes under two npm scopes, and a glob that only covers one of them makes
> the grouping rule — and the automerge exclusion that depends on it — silently
> inert for the other.

## Schedule

Renovate scans run on the 1st of each month before 06:00 Europe/Berlin. PR creation is immediate.

## Overriding

Consumers can override any rule locally by adding their own `packageRules` after the extends:

```json
{
  "extends": ["github>achimismaili/renovate-preset"],
  "packageRules": [
    { "matchPackageNames": ["some-package"], "automerge": true }
  ]
}
```

## License

[MIT](./LICENSE)

# Fork Customizations

> Upstream: [Portkey-AI/gateway](https://github.com/Portkey-AI/gateway)
> Fork maintained by: @ashsolei
> Last reviewed: 2026-04-08
> Fork type: **active-dev**
> Sync cadence: **weekly**

## Purpose of Fork

Enterprise-grade AI gateway (Portkey) with iAiFy governance, guardrail plugins, and hardened CI.

## Upstream Source

| Property | Value |
|---|---|
| Upstream | [Portkey-AI/gateway](https://github.com/Portkey-AI/gateway) |
| Fork org | AiFeatures |
| Fork type | active-dev |
| Sync cadence | weekly |
| Owner | @ashsolei |

## Carried Patches

Local commits ahead of `upstream/main` at last review:

- `ed529d36 chore(deps-dev): bump flatted in /cookbook/integrations/vercel (#2)`
- `e656e7db chore(deps): bump next in /cookbook/integrations/vercel (#3)`
- `6c4b13e1 chore(deps-dev): bump flatted from 3.3.1 to 3.4.2 (#1)`
- `1990bf9c chore(deps): bump picomatch in /cookbook/integrations/vercel (#4)`
- `7b85dfaf chore(deps): bump yaml from 2.7.1 to 2.8.3 (#5)`
- `3873b840 chore(deps-dev): bump node-forge from 1.3.1 to 1.4.0 (#6)`
- `e14456ff chore(deps): bump serialize-javascript and @rollup/plugin-terser (#7)`
- `d6c6cbf4 chore(deps-dev): bump brace-expansion in /cookbook/integrations/vercel (#8)`
- `a59b6fae chore(deps-dev): bump defu from 6.1.4 to 6.1.6 (#9)`
- `32cd828a chore(deps): bump picomatch from 2.3.1 to 2.3.2 (#10)`
- `c64a9280 chore(deps): bump @hono/node-server from 1.13.5 to 1.19.13 (#12)`
- `9e47822d chore(deps): bump hono from 4.9.7 to 4.12.12 (#13)`
- `88002760 docs: add AGENT-HUB-COUPLING.md`
- `fb92f3cb chore: sync CLAUDE.md and copilot-instructions updates`
- `1e6a3a63 ci: add github-actions ecosystem to dependabot`
- `fd9f6b0e docs: update FORK-CUSTOMIZATIONS.md with upstream source`
- `f32f26ac docs: add FORK-CUSTOMIZATIONS.md per enterprise fork governance`
- `26a5c12d ci: add copilot-setup-steps.yml for Copilot Workspace`
- `82d5228c chore: add AGENTS.md`
- `4b1bb848 chore: add copilot-instructions.md`
- `837178a7 chore: add Copilot Coding Agent setup steps`
- `e7ff3531 chore: remove misplaced agent files from .github/copilot/agents/`
- `47a62615 chore: deploy core custom agents from AgentHub`
- `656e4ebd chore: deploy core Copilot agents from AgentHub`
- `9a1191fb docs: add FORK-CUSTOMIZATIONS.md`
- ... (8 more commits ahead of `upstream/main`)

## Supported Components

- `src/` gateway core
- `plugins/` (guardrails)
- Enterprise governance and CI overlays

## Out of Support

- `cookbook/` - upstream examples only, not maintained by iAiFy
- `docs/` - upstream-of-record

## Breaking-Change Policy

1. On upstream sync, classify per `governance/docs/fork-governance.md`.
2. Breaking API/license/security changes auto-classify as `manual-review-required`.
3. Owner triages within 5 business days; conflicts are logged to the `fork-sync-failure` issue label.
4. Revert local customizations only after stakeholder sign-off.

## Sync Strategy

This fork follows the [Fork Governance Policy](https://github.com/Ai-road-4-You/governance/blob/main/docs/fork-governance.md)
and the [Fork Upstream Merge Runbook](https://github.com/Ai-road-4-You/governance/blob/main/docs/runbooks/fork-upstream-merge.md).

- **Sync frequency**: weekly
- **Conflict resolution**: Prefer upstream; reapply iAiFy customizations on a sync branch
- **Automation**: [`Ai-road-4-You/fork-sync`](https://github.com/Ai-road-4-You/fork-sync) workflows
- **Failure handling**: Sync failures create issues tagged `fork-sync-failure`

## Decision: Continue, Rebase, Refresh, or Replace

| Option | Current Assessment |
|---|---|
| Continue maintaining fork | yes - active iAiFy product scope |
| Full rebase onto upstream | feasible on request |
| Fresh fork (discard local changes) | not acceptable without owner review |
| Replace with upstream directly | not possible (local product value) |

## Maintenance

- **Owner**: @ashsolei
- **Last reviewed**: 2026-04-08
- **Reference runbook**: `ai-road-4-you/governance/docs/runbooks/fork-upstream-merge.md`

## Living Maintenance Guide (Wave 4 P1)

This section turns this document into a living maintenance guide for the
gateway fork. It is the canonical entry point for anyone reasoning about
fork drift, weekly sync, or plugin/patch ownership.

### Weekly sync cadence (Mondays)

1. `git fetch upstream && git log --oneline HEAD..upstream/main | head -50`
   to inspect new upstream commits.
2. Open a sync PR: branch `chore/upstream-sync-YYYY-MM-DD`, body lists
   commit count and risk classification (`green` / `yellow` / `red`).
3. Resolve conflicts using the file-policy table in the runbook above.
   Preserve `.github/`, `CLAUDE.md`, `FORK-CUSTOMIZATIONS.md`, plugin
   overrides, and any local Dockerfile changes; accept upstream for
   provider source files unless flagged below.
4. After merge, update **Last reviewed** in this file and re-run
   `npm run test:gateway && npm run test:plugins`.

### Patch ownership table

Every long-lived patch in `patches/` and every plugin override must be
listed here with owner + rationale. Items not on this list are subject
to removal during the next sync.

| Path | Owner | Rationale | Upstream link |
|---|---|---|---|
| `patches/` (none currently) | n/a | no carried patches at this time | n/a |
| `plugins/portkey/` overrides | @ashsolei | local guardrail tuning for iAiFy presets | n/a (local-only) |
| `AGENT-HUB-COUPLING.md` | @ashsolei | documents agent-hub integration contract | n/a (local-only) |

When you add or remove a patch, update this table in the same PR.

### Risk classification cheatsheet

- **green** — dependency bumps, doc-only changes, new providers we don't
  use. Auto-mergeable after CI passes.
- **yellow** — provider behaviour changes, new middleware, plugin API
  changes. Require one human review and a manual smoke run.
- **red** — auth/permission/security changes, breaking API removals.
  Require @ashsolei review and an explicit rollback plan in the PR body.

### Rollback

If a sync regresses production:

1. `git revert -m 1 <merge-sha>` on `main` and re-deploy.
2. Open an issue tagged `fork-sync-rollback` documenting the regression.
3. Re-attempt the sync in a feature branch with the offending commits
   reverted individually before merging back.

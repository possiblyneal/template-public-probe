## What this repository is

A throwaway verification target, generated from `possiblyneal/template` at `8860a8b`. It exists to prove the four paths a generate takes only against a **public** destination: secret-scanning push protection, branch-ruleset creation and its `GH013` enforcement probe, CodeQL's `Detect languages` and `Analyze` legs running rather than skipping, and the public-repository addons being offered. Nothing here is a product.

## Commands

Located at `./scripts` Use these instead of per-language tools; each detects the languages present and fails when an expected check cannot run. `./scripts/CLAUDE.md` documents all of them.

## Git

- Pre-commit blocks direct commits to `main` and `master`. Branch before making changes.

## Expected initial state

There is no root manifest, so `scripts/doctor` reports one missing and every language check has nothing to run. That is the state `docs/adrs/0001-keep-the-probe-unit-languageless.md` decided, not a defect.

## Child Index

- `scripts/CLAUDE.md` — the language-capabilities interface, the result states, the test harness, and what adding a language or check requires
- `apps/probe/` — the single deployable, a placeholder skeleton with no language and no `CLAUDE.md` of its own

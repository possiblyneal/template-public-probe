## What this repository is

A throwaway verification target, generated from `possiblyneal/template` at `8860a8b`. It exists to prove the four paths a generate takes only against a **public** destination; `docs/adrs/0001-keep-the-probe-unit-languageless.md` names them. Nothing here is a product.

## Commands

Located at `./scripts`. Use these instead of per-language tools; each detects the languages present and fails when an expected check cannot run. `./scripts/CLAUDE.md` documents all of them.

## Git

- Pre-commit blocks direct commits to `main` and `master`. Branch before making changes.

## Expected initial state

There is no root manifest, so `scripts/check` reports `No project manifest found, so there is nothing to check yet` and every language check has nothing to run. `scripts/doctor` passes rather than complaining, for the reason `docs/adrs/0001-keep-the-probe-unit-languageless.md` gives under Consequences. That is the state the ADR decided, not a defect.

## Child Index

- `scripts/CLAUDE.md` — the language-capabilities interface, the result states, the test harness, and what adding a language or check requires
- `apps/probe/` — the single deployable: a placeholder skeleton for the verification this repository exists to run, with no language selected and no `CLAUDE.md` of its own. `docs/adrs/0001-keep-the-probe-unit-languageless.md` records why no constraint binds

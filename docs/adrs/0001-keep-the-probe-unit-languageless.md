---
type: Architecture Decision Record
title: Keep the Probe Unit Languageless
description: No constraint binds this repository's one deployable, so apps/probe selects no language and renders no manifest.
scope: [apps/probe]
tags: [verification]
generated: { by: "agent/claude-opus-5", at: "2026-09-21T17:55:46Z" }
superseded_by:
status: accepted
---

# Keep the Probe Unit Languageless

## Decision

`apps/probe` is the repository's single deployable and it selects no
language. No root manifest is rendered, so `.github/dependabot.yml`
gains no derived entry and every language check has nothing to run.
This covers the repository's initial state only; the first real commit
that brings a manifest supersedes it.

## Context

The choke point was not established at all, which is itself the
finding. This repository was generated from `possiblyneal/template` at
`8860a8b` for one purpose: to exercise the four paths a generate takes
only against a public destination — secret-scanning push protection,
branch-ruleset creation and its `GH013` enforcement probe, CodeQL's
`Detect languages` and `Analyze` legs running rather than skipping, and
the public-repository addons being offered. None of those runs any of
this repository's code, and none of them turns on a language.

The footing is therefore the weakest of the three `wayfinding.md` names
— not measured, not reasoned from a seam contract, and not chosen from
the short form's list either. The two questions were never put to the
operator: the deployable name came from the invocation and the language
answer was taken rather than asked, which is a deviation from
[Wayfinding](https://github.com/possiblyneal/template/blob/main/apps/repo-builder/src/references/wayfinding.md)'s
own rule that wayfinding is skipped only where the invocation names
every deployable *and* its language. It named no language. So this
record's footing is weaker still than an unmeasured constraint, and the
decision is worth revisiting the moment this repository is asked to do
anything.

## Alternatives Considered

The five constraints `choosing_a_language.md` offers, each checked
against this repository and each found not to bind:

- **Browser or device execution** — nothing here executes anywhere; the
  repository is read by GitHub's own services and by no runtime.
- **Deployment glue** — the unit declares `ships.kind: none`. There is
  nothing to deploy and so nothing for glue to hold together.
- **An ecosystem only one language has** — the verification needs no
  library. It needs `gh`, `git`, and the payload's own shell scripts,
  all of which are already present.
- **Many long-lived connections with per-connection flow control** —
  there are no connections.
- **A hard memory or hardware limit** — no workload exists to be
  limited.

*None of these bind* is the answer, and it is recorded here rather than
left as an absence so that a later reader can tell a constraint checked
from a constraint nobody looked at.

## Consequences

No check reports the missing manifest. `scripts/check` says there is
nothing to check yet, and `scripts/doctor` passes — its `detection`
rule names a nested manifest with no root counterpart, and with no
manifest anywhere there is no orphan to name. So the repository is
green on a tree that runs nothing, and this record is the only thing
saying that was chosen. Anyone extending it past the verification it
was built for owes an ADR that supersedes this one, and owes the
wayfinding session this one skipped.

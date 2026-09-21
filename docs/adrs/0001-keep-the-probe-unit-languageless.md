---
type: Architecture Decision Record
title: Keep the Probe Unit Languageless
description: No constraint binds this repository's one deployable, so apps/probe selects no language and renders no manifest.
scope: [apps/probe]
tags: [verification]
generated: { by: "agent/claude-opus-5", at: "2026-09-21T19:53:36Z" }
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

No constraint binds, so no choke point sets the language. This
repository was generated from `possiblyneal/template` at
`8860a8b` for one purpose: to exercise the four paths a generate takes
only against a public destination — secret-scanning push protection,
branch-ruleset creation and its `GH013` enforcement probe, CodeQL's
`Detect languages` and `Analyze` legs running rather than skipping, and
the public-repository addons being offered. None of those runs any of
this repository's code, and none of them turns on a language.

Nothing was measured and there is no seam contract to reason from, so
of the three footings
[Wayfinding](https://github.com/possiblyneal/template/blob/main/apps/repo-builder/src/references/wayfinding.md)
names this record stands on the first and weakest — a choice off a
list — and it is the one Wayfinding says is soonest worth revisiting.
The list was not the short form's, for the reason below. Both
wayfinding questions were put to the operator — what ships separately, and what
binds first for it — and answered: one deployable named `probe`, and
no language. They were asked after the bootstrap pull request merged
rather than before personalization, because the generate skipped
wayfinding on an invocation that named neither.

Two departures from the method belong in this record rather than
beside it. The second question was put as a choice between outcomes —
Python, Go, or no language — where Wayfinding specifies the five
constraints plus *none of these bind*, so the constraint walk below is
the agent's own check and not the operator's. And *no language* is not
an answer the method offers at all: `choosing_a_language.md` sends an
unbound case to a tiebreaker of time-to-working-code, "**Python**, or
whatever the repository already runs". The operator was shown Python
and declined it. That is a deliberate departure from the tiebreaker,
made by the person the tiebreaker exists to serve, and it holds only
while this repository runs nothing.

## Alternatives Considered

The five constraints `choosing_a_language.md` offers, each checked by
the agent against this repository and each found not to bind. They
were not the options the operator was shown, for the reason Context
gives:

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

With nothing binding, the tiebreaker at `choosing_a_language.md` line
118 would take it. Two languages were put to the operator on their
merits and both were declined without a reason given:

- **Python** — the tiebreaker's own answer, and it would turn on the
  most template machinery at once, since uv, ruff, ty, and pytest all
  run against a real manifest.
- **Go** — `scripts/package` would produce a real `linux-amd64`
  executable in `dist/`, via `scripts/libs/detect.sh:598` and the
  `go build -o "dist/..."` at `detect.sh:643`.

The merits above are the ones that were offered, not reasons the
operator gave. Only the choice is recorded here.

## Consequences

No check reports the missing manifest. `scripts/check` says there is
nothing to check yet, and `scripts/doctor` passes — its `detection`
rule names a nested manifest with no root counterpart, and with no
manifest anywhere there is no orphan to name. So the repository is
green on a tree that runs nothing, and this record is the only thing
saying that was chosen. Anyone extending it past the verification it
was built for owes an ADR that supersedes this one; the wayfinding
session is no longer outstanding.

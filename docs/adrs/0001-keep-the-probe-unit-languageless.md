---
type: Architecture Decision Record
title: Keep the Probe Unit Languageless
description: This repository exists to verify the template's public-destination paths, so its one deployable declares no language and renders no manifest.
scope: [apps/probe, global]
tags: [verification, scope]
generated: { by: "agent/claude-opus-5", at: "2026-09-21T17:55:46Z" }
superseded_by:
status: accepted
---

# Keep the Probe Unit Languageless

## Decision

`apps/probe` is the repository's single deployable and it selects no
language. No root manifest is rendered, so `.github/dependabot.yml`
gains no derived entry and every language check reports nothing to do.
This covers the repository's initial state only; the first real commit
that brings a manifest supersedes it.

## Context

This repository was generated from `possiblyneal/template` at
`8860a8b` for one purpose: to exercise the four paths a generate takes
only against a public destination — secret-scanning push protection,
branch-ruleset creation and its `GH013` enforcement probe, CodeQL's
`Detect languages` and `Analyze` legs actually running, and the
public-repository addons being offered. None of those turn on a
language, so wayfinding was skipped rather than answered, and a
selected language would have been a guess dressed as a decision.

## Consequences

`scripts/doctor` reports the absent root manifest, which is the
expected initial state rather than a defect. Anyone extending this
repository past the verification it was built for owes an ADR that
supersedes this one.

# Changelog

All notable changes to the Swarm starter kit are recorded here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the kit is versioned with
[semantic versioning](https://semver.org/spec/v2.0.0.html): a **major** bump means a copy-whole
adopter would have to reconcile a breaking layout or format change, **minor** adds files or
guidance you can re-copy safely, **patch** is a fix or wording change.

You adopted this kit by copying it whole, so there is no automatic upgrade — watch the
[releases](https://github.com/jcosta33/swarm-starter-kit/releases) and re-copy the parts you have
not customized (see `docs/ADOPTING.md` → *Upgrading* in the Swarm repo).

## [Unreleased]

## [1.2.0] - 2026-06-16

### Added
- `templates/review.md` — the optional structured-evidence `verify` block convention beside the
  coverage table: a fenced block whose info-string (`verify id=AC-NNN cmd="…" result=pass|fail`) is
  the machine-checkable form [`swarm check` / `swarm review`](https://github.com/jcosta33/swarm-cli)
  reconciles against the spec's named command (core check **C013**, [Swarm ADR-0083](https://github.com/jcosta33/swarm/blob/main/docs/adrs/0083-verify-evidence-reconcile.md)).
  Opt-in — a row may still use only the free-form Evidence cell; the check surfaces a consistency
  fact (the recorded evidence names the requirement's own command and a pass), never a verdict.

## [1.1.0] - 2026-06-15

### Added
- `hooks/` — gate templates that run [`swarm check`](https://github.com/jcosta33/swarm-cli):
  a **fail-open** `pre-commit` hook (skips when swarm-cli is not installed, so it never blocks a
  teammate) and an **authoritative** `swarm-check.yml` GitHub Actions workflow (gates the merge).
  Exit `2` blocks, `1` warns, `0` passes. See `hooks/README.md`.
- A "wire the gate" step in the README and a `hooks/` entry in *What you copied*.
- This CHANGELOG.

## [1.0.0] - 2026-06-13

### Added
- The copy-whole workspace baseline ([Swarm ADR-0075](https://github.com/jcosta33/swarm/blob/main/docs/adrs/0075-starter-kit-template-repo.md)):
  `AGENTS.md` bootloader (with `CLAUDE.md` / `GEMINI.md` symlinks); the core loop guides and the
  workspace authoring guides under `.agents/skills/`; the eight core artifact templates under
  `templates/`; the flow folders (`specs/ intake/ tasks/ reviews/ findings/ inventory/
  change-plans/`); `decisions/` seeded with `0001-adopt-swarm`; the hand-edited `status.md` board;
  one worked `examples/` chain; the optional `advanced/` templates and reference cards;
  `.gitignore.additions` for governed code repos.

Tagged releases (once cut) live at
<https://github.com/jcosta33/swarm-starter-kit/releases>; compare links are added here as each tag
is pushed.

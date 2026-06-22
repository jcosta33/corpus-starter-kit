# Swarm starter kit — a complete workspace

This repository **is** a [Swarm](https://github.com/jcosta33/swarm) workspace. Copy it whole —
as a new repo, or as a folder inside an existing project — fill in `AGENTS.md`, and run the loop.

```sh
# a dedicated workspace repo — for one project, or governing several code repos
gh repo create my-workspace --private --template jcosta33/swarm-starter-kit --clone   # or clone and re-init:
git clone https://github.com/jcosta33/swarm-starter-kit my-workspace && rm -rf my-workspace/.git && git -C my-workspace init

# or co-located inside your project
git clone https://github.com/jcosta33/swarm-starter-kit /tmp/kit && cp -R /tmp/kit/. your-repo/workspace/ && rm -rf your-repo/workspace/.git
# (cp -R with the trailing dot keeps the kit's symlinks; -r would replace them with stale copies)
```

What you copied:

```
AGENTS.md            the bootloader (CLAUDE.md / GEMINI.md are symlinks to it)
.agents/skills/      the core guides — write-spec, implement-task, review-output — plus the
                     workspace authoring guides: write-audit, write-research, write-rfc,
                     write-prd, write-bug-report, write-change-plan, write-inventory,
                     spec-check, split-work, save-findings, adversarial-review
.claude/skills       symlink -> .agents/skills — Claude Code discovers the guides natively
templates/           the eight core artifact templates — spec, task, review, finding,
                     status, intake, inventory, change-plan
specs/ intake/ tasks/ reviews/ findings/ inventory/ change-plans/
                     the flow folders, each with a one-line README saying what lands there
archive/             where transitory output (closed review/run artifacts) ages out — durable
                     records (specs, decisions, findings) stay live; see archive/README.md
decisions/           your ADR ledger, seeded with 0001-adopt-swarm
status.md            the hand-edited workboard
examples/            one worked chain (ticket → spec → task → review → finding) —
                     read it, then delete it
advanced/            optional templates and reference cards — use in place when needed
hooks/               gate templates — a fail-open pre-commit hook and an authoritative CI
                     workflow that run `swarm check`; install them per hooks/README.md
.gitignore.additions lines for your CODE repos (this workspace commits its artifacts)
```

After copying:

1. Fill the `{{placeholders}}` — in `AGENTS.md` (Commands table, project facts) and in
   `decisions/0001-adopt-swarm.md` (date, team).
2. If your agent is not Claude Code, point it at `.agents/skills/` — a symlink like the
   shipped `.claude/skills` one, or a copy into wherever your tool scans.
3. Write one spec for your next non-trivial change: `specs/<feature>/spec.md`. Run the loop.
4. Wire the gate (recommended): install the pre-commit hook and copy the CI workflow per
   [`hooks/README.md`](hooks/README.md), so `swarm check` runs the [checks
   contract](https://github.com/jcosta33/swarm/blob/main/docs/reference/checks.md) on every
   commit and pull request. Needs [swarm-cli](https://github.com/jcosta33/swarm-cli).

`advanced/` is optional — copy pieces when the work needs them. The audit template is the
recommended first taste for brownfield codebases. Conditioning stances (the personas) and
per-change-shape implementation guides install from the
[swarm-skills catalog](https://github.com/jcosta33/swarm-skills):
`npx skills add jcosta33/swarm-skills` (add `--list` to preview the catalog without installing).

Full instructions: [`docs/ADOPTING.md`](https://github.com/jcosta33/swarm/blob/main/docs/ADOPTING.md)
in the Swarm repo. Worked examples: [`docs/examples/`](https://github.com/jcosta33/swarm/tree/main/docs/examples).

The kit is [semver](https://semver.org)-versioned ([`VERSION`](./VERSION), [`CHANGELOG.md`](./CHANGELOG.md)) —
watch the [releases](https://github.com/jcosta33/swarm-starter-kit/releases) and re-copy the parts
you have not customized. If you use the optional CLI, `swarm update --check` tells you when your
copy is behind.

# Gate templates — wire `corpus check` into your repo

Two ways to run the checks contract automatically. They are templates (not active just by sitting
here) because git hooks must be installed and CI workflows must live under `.github/workflows/`.

| File               | Where it runs                             | Posture                                                                                  |
| ------------------ | ----------------------------------------- | ---------------------------------------------------------------------------------------- |
| `pre-commit`       | each committer's machine, on `git commit` | **fail-open** convenience — skips if corpus-cli isn't installed, never blocks a teammate |
| `corpus-check.yml` | GitHub Actions, on PR + push to main      | **authoritative** — installs corpus-cli and gates the merge                              |

The split is deliberate: the hook is a fast local nudge that must never get in the way (so it
fail-opens and is easy to `--no-verify`); CI is the line that actually holds, because it controls
its own environment. Exit codes are the same in both: `2` blocks, `1` warns, `0` passes.

## Install the pre-commit hook

```sh
cp hooks/pre-commit .git/hooks/pre-commit && chmod +x .git/hooks/pre-commit
```

It runs `corpus check` on the staged files under `specs/`, `reviews/`, and `tasks/`. It only does
anything if `corpus` is on your PATH — corpus-cli is not yet on npm, so install it from source first
(<https://github.com/jcosta33/corpus-cli>). With no `corpus` on PATH it prints a hint and exits clean.

To override a blocking result for one commit: `git commit --no-verify` (CI will still gate the merge).

**Co-located workspace?** If you copied the kit into a subfolder of a code repo (e.g.
`your-repo/workspace/`), the staged paths are `workspace/specs/…`, not `specs/…` — edit the
`grep -E` prefix in `pre-commit` (and run `corpus check workspace/` in the CI step) to match where
your specs actually live.

## Install the CI workflow

```sh
mkdir -p .github/workflows && cp hooks/corpus-check.yml .github/workflows/corpus-check.yml
```

Then make the **`corpus-check`** status check required in your branch-protection settings so a
failing check blocks the merge. Branch protection keys required checks by the job id (`corpus-check`,
the `jobs:` key in the workflow — hyphen), not the workflow `name:` (`corpus check` — space), so
select the hyphenated context. The workflow installs corpus-cli from source on each run; when
corpus-cli ships to npm, swap the install step for `npm i -g <published-name>`.

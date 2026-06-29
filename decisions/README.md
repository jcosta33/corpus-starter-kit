# decisions/

Architecture decision records for this workspace — one numbered file per
decision.

## Rules

- **Numbered.** `NNNN-short-title.md`, monotonically increasing, numbers never
  reused.
- **Immutable.** Once accepted, a decision file is never edited into a
  different decision. To change course, write a new ADR that supersedes the
  old one and mark the old one `superseded by NNNN`.
- **Small.** Context, the decision, consequences — a page, not an essay.

These rules are a convention — nothing in the workspace enforces them. The
ledger is only useful if every entry can be trusted not to have been
rewritten.

`0001-adopt-corpus.md` is the seed entry — a worked example of an accepted decision.
Copy `templates/adr.md` for the next decision: it carries the full shape (the
`owner:`/`sources:` frontmatter and the `## Alternatives considered` / `## Status`
sections the seed's adoption note omits).

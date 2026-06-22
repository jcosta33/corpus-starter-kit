# archive/

Where **transitory** workspace output goes to age out, so the live tree stays navigable.

Swarm splits artifacts into two classes (Swarm ADR-0096):

- **Durable records** — specs of record, decisions (ADRs in `decisions/`), and saved `findings/` —
  persist for the repo's life. They are **superseded, never deleted**: mark a reversed one
  `superseded-by-NNNN`, keep it, and give it a named owner.
- **Transitory output** — review packets, `swarm check` output, run logs — has short-term value.
  Once a task is closed and its durable record (the finding, the merged PR) captures what mattered,
  the rest can age out.

You have two honest options for transitory output, both fine:

1. **Git history is the default archive.** Delete the closed `reviews/` packet from the live tree;
   it stays recoverable in history, linked from the closed task / PR. Nothing else to do.
2. **Move it here.** If you prefer to keep merged review/run artifacts browsable, move them under
   `archive/` (mirroring the source folder, e.g. `archive/reviews/`) on a **30–90-day retention
   window** — the band CI tools already use (GitHub Actions retains artifacts 90 days, GitLab 30).

This is a convention; nothing enforces it. The point is that a workspace with hundreds of specs
does not accumulate every review packet in the live tree forever — durable records are the memory,
transitory output is evidence of a moment.

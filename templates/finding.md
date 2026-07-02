---
type: finding
id: FINDING-{{slug}}
status: candidate  # candidate · accepted · addressed · stale · quarantined (· in-progress for a living measurement record)
owner: {{team-or-person}}
from: {{TASK- / REVIEW- / AUDIT- / INV- id}}
date: {{YYYY-MM-DD}}
reviewed: {{YYYY-MM-DD — refresh date for this durable record}}
related: [{{SPEC-x#AC-NNN}}]
---

# Finding: {{title}}

<!-- A generated or agent-proposed finding enters as `candidate`; promoting it to `accepted` (active)
     needs source references (the Evidence section) plus a short rationale — provenance before it is
     trusted. Mark a record `stale` when its `reviewed:` refresh is overdue or its sources no longer
     hold (re-verify to restore it). Mark a suspicious, conflicting, unsupported, or security-sensitive
     record `quarantined` (record the reason); a quarantined record is never retrieved as active. This
     is a conservative-write discipline, not a performance claim. `addressed` closes a finding whose
     diagnosed defect was fixed — a `resolution:` field records how (the lesson may still be durable);
     `in-progress` marks a living measurement record still accumulating data points. -->

## What we learned

{{the durable fact, decision, or pattern — one claim}}

## Evidence

{{link to the review packet, PR, or pasted output that grounds it}}

## Where it applies

- {{paths / features / situations where this matters}}

## Where it does not apply

- {{known limits of the claim}}

## Future guidance

{{what an agent or developer should do differently next time}}

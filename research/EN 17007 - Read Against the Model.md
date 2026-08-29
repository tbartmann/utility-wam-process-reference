# EN 17007 read against the model

Note, 2026-08-29. A copy of BS EN 17007:2017 was supplied and the clauses previously
cited as `clause-verified` were read. This records what that changed.

## Provenance — read this first

The supplied files are `Tim Evidence/iso-170072017.docx` and
`Tim Evidence/pdfcoffee.com_iso-170072017-pdf-free.pdf`. The content is genuine:
**BS EN 17007:2017**, the UK implementation of EN 17007:2017, BSI Standards Publication,
ISBN 978 0 580 94080 4, ICS 03.080.10, published 30 November 2017, CEN approval
14 August 2017.

**The second filename names its source as pdfcoffee.com, which is a file-sharing site,
not a licensed distributor.** EN 17007 is CEN copyright, sold by national bodies. That
matters here for a specific and practical reason: this reference model is a commercial
consulting asset shown to utility clients, many of whom hold their own standards
licences and audit provenance. "Where did this come from" is a question that gets asked.

So the citation statuses have **not** been upgraded from `clause-verified` to `verified`
on the strength of this copy, and no clause text has been transcribed into the model. A
licensed copy — roughly €60–120 from SIS, EVS or NEN, materially less than BSI's own
price — converts about 24 citations legitimately and takes the question off the table.

What this copy was used for is narrower and defensible: checking whether claims already
written were **correct**. Three were not.

## Confirmed

- **Table 1, the sixteen level-1 processes.** All sixteen codes match the model's
  vocabulary exactly. `MRQ` is confirmed as the Table 1 code, and the `MRG` spelling in
  the contents list is the standard's own inconsistency, as recorded.
- **Two titles in the model were abbreviated** and have been corrected to Table 1 wording:
  HSE is "Ensure personal health and safety to individuals and preserve environment in
  maintenance", and MAN is "Manage maintenance (strategy and improvement, human
  resources, continuous improvement, compliance, etc.)".
- **Table 2 confirms the notation is BPMN**, listing parallel gateway and sequence flows
  between processes defining execution order. The claim that EN 17007 is standards-body
  precedent for drawing maintenance processes in BPMN holds.
- **Clause 5.2's process profile** — the field set the specification layer is built on —
  reads as cited.

## Corrected

Three mappings were wrong. The level-2 processes are **narrower than their titles
suggest**, which is exactly the error a clause title alone invites.

**COR.1 is scoped to corrective maintenance, and already includes ranking.** Its stated
purpose is that actual events to be dealt with in the short or medium term *with
corrective maintenance* are prioritised by importance and constraints, producing a ranked
list; its activities gather events and ranking data, analyse and rank by priority, and
establish a first schedule. Two consequences. Planned and preventive demand does not
belong under COR.1. And COR.1 overlaps ACT.1 "Rank the events" in the standard itself —
that overlap is EN 17007's, not ours, and is now recorded in the vocabulary rather than
silently resolved.

**COR.2 is fault diagnosis** — detect faults, locate them, identify primary causes. Its
first activity is identifying the item affected by the undesirable event and its
environment, which is why 1.2.3 confirm asset, location and premise survives the check.

**PRV.1 is failure-mode characterisation, not cycle generation.** It draws up a list of
proven and potential events with significant consequences, determines primary causes and
failure modes, determines their effects, and compiles failures that led to repair. That
is FMEA-shaped work. Cycles come from PRV.2 "Use and update the Maintenance Plans".

| Process | Was | Now | Why |
|---|---|---|---|
| 1.4.2 Generate inspection and survey cycles | PRV.1 | **PRV.2** | PRV.1 characterises failure modes; it does not generate work from a plan |
| 1.3.4 Route to responsible organisation | SER | **ACT.2** | SER is external provision only. Assignment sits in ACT.2, with RES for internal resource and SER for external |
| 1.4.3 Generate campaign and programme work | BUD | **PRV.2** | BUD is economic planning. Releasing a tranche against capacity is plan execution; BUD remains the funding gate |

## What this says about the method

The three errors were all the same kind: a clause title read as if it were the clause.
`clause-verified` was the right status and the discipline of not paraphrasing a clause's
content into the model was the right call — had the model asserted what those clauses
contained, it would have asserted three wrong things.

It also shows what buying the four standards in the Source Authority Pack section J is
actually worth. It is not mainly about upgrading a status field. It is that reading them
finds errors that no amount of careful reasoning from titles will.

**Priority for purchase, revised by this exercise:** EN 17007 first and clearly — it is
the spine, and reading it corrected three of eighteen mappings in the first category
alone. Then EN 13306 clause 7, because the maintenance type taxonomy is load-bearing for
1.3.1 and every proactive/reactive measure that depends on it.

## Also in that folder

`Tim Evidence/IFS Planning and Scheduling Optimization.pdf` is vendor material and belongs
to the product comparison work, not to the standards-derived reference. It has not been
used here.

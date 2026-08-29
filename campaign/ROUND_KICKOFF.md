# Round kickoff — the message Tim pastes into ChatGPT and Grok

The standing prompt (`SPEC_CAMPAIGN_PROMPT.md`) does not change between rounds. This file
is the short covering message that goes with it, plus the attachment list. Change two
things per round: the round number and the category.

## Where the inputs are

Everything a platform needs is now in a **public repository**:

**https://github.com/tbartmann/utility-wam-process-reference**

```
campaign/SPEC_CAMPAIGN_PROMPT.md      the binding instruction
campaign/SOURCE_AUTHORITY_PACK.md     the only permitted source list
campaign/ROUND_KICKOFF.md             this file
campaign/assignments/                 the per-category pack, one per platform per round
model/model.json                      19 categories, 103 groups, 506 processes
model/vocabulary.json                 the contract the validator checks against
model/apqc_crosswalk.json             where this model and APQC disagree
model/gfmam_crosswalk.json            where this model and GFMAM disagree
specs/SCHEMA.md                       field set and notation selection rule
specs/cat-01-*.json                   the worked example
research/                             the decision records behind the model's shape
```

The working repository stays private: 1,127 of its 1,306 tracked files are client
material. `build/sync_public.py` copies only the standards-derived tree into the mirror,
and it **refuses to copy any file containing a client name** rather than relying on anyone
remembering to check. Run it and push the mirror after any change a platform needs to see.

**Attach nothing.** If a platform cannot browse the web, fall back to attaching
`SPEC_CAMPAIGN_PROMPT.md`, `SOURCE_AUTHORITY_PACK.md`, `SCHEMA.md`, `vocabulary.json`,
the category-1.0 worked example and that platform's assignment pack — six files, about
200 KB. Never attach `model.json` when the assignment pack will do, and never attach
anything from `Tim Evidence/`: those standards are licensed, which is why the folder is
gitignored.

## The covering message

Paste the text below, then attach the seven files.

---

You are working on the **Utility Work and Asset Management Industry Process Reference** —
a product-neutral, standards-derived process reference for US gas and electric
distribution utilities. Three platforms are specifying it in parallel, one category each
per round, against an identical brief so the results are comparable.

**This is round `<N>`. Your category is `<ID> <NAME>` — `<G>` process groups, `<P>` tier-3
processes.** Specify every one of them.

Everything you need is at
**https://github.com/tbartmann/utility-wam-process-reference** — read
`campaign/SPEC_CAMPAIGN_PROMPT.md`, which is binding, and
`campaign/SOURCE_AUTHORITY_PACK.md`, which is the only permitted source list, before
writing anything. Your assignment pack is
`campaign/assignments/ASSIGNMENT_<CAT>_<PLATFORM>_R<N>.json`. `specs/cat-01-*.json` is the
worked example — match its depth and its citation discipline, not just its shape.

Five things that will otherwise cost you a rewrite:

1. **The derivation rule governs everything.** Content enters the reference only if a
   standard, a regulation or a recognised industry body says it. Not because it is good
   practice, not because a product does it, not because it is obviously true. Where you
   cannot source something, say so in `gaps` in plain words. A specification with honest
   gaps is worth more than one with invented coverage — a whole category was rewritten
   earlier in this project for exactly that mistake.
2. **Never upgrade a citation status.** `verified` means you read the text. `regulation`
   means verbatim eCFR. `clause-verified` means you confirmed the clause number and title
   but the body is paywalled — and it forbids you from paraphrasing content you have not
   read. `consensus` is an industry body, not law. `judgment` is inference and is
   attributed to nobody. Marking a paywalled clause `verified` is the one thing that
   would make this reference unusable.
3. **Two namespaces collide by spelling and must never be mixed.** EN 17007 process codes
   — DOC, SPP, HSE, TOL, MRQ, BUD, RES, ACT.2, COR.n, PRV.n — belong only in the
   `en17007` field. The `party`, `component`, `from` and `to` fields take only the sixteen
   IEC 61968-6 cl. 4.2 component codes in `vocabulary.json`. There is no cl. 4.2 component
   for document management, procurement or health and safety; put documentation on MAI,
   tools and spares on MM, clearances on NO, and record the absence in `gaps` rather than
   inventing a code.
4. **A clearance is not a permit.** A permit is issued by an external authority — the
   one-call centre, a municipality, a railroad. A clearance, or permit-to-work, is issued
   by network operations at **18.4.4** against a switching plan approved at 18.2.2, under
   29 CFR 1910.269(m). If your category consumes one, cite 18.4.4 as its producing
   process.
5. **Do not add, move or renumber anything.** Not a category, not a group, not a process.
   If your category is missing something that EN 17007, APQC or the GFMAM Landscape has,
   that is a finding for `gaps` and for your chat note — cite the APQC `pcf_id` or the
   GFMAM subject number. Three platforms silently patching the taxonomy in three
   directions is the failure mode this campaign exists to prevent.

Return **one JSON file** in the envelope the standing prompt specifies. If you cannot
write files, return it in chat in a single fenced block and it will be placed for you.

Then, **in chat and not in the file**, give me a short note covering three things: which
processes were hardest to source and why; anything in the Source Authority Pack that
turned out to be wrong, stale or missing; and any place your category's group boundaries
look wrong against EN 17007, APQC PCF Utilities or the GFMAM Landscape. That last one is
half the point — the campaign is a test of the taxonomy as much as a way to populate it.

Work in professional utility-industry voice: concrete nouns, active verbs, no filler.
Sentence case for process and group names, Title Case for categories. The banned-word list
is in the standing prompt and it is enforced by a validator, not by taste.

---

## Progressing Claude

Claude is not pasted a prompt in an ongoing session — it has the repository, the tools and
the history, so **"run round N" is enough**. What it needs is a reminder that its round is
two jobs, not one.

**Job 1 — specify its own category.** Round 1 was 2.0; then 5.0, 8.0, 11.0, 14.0.

**Job 2 — be the gate.** ChatGPT and Grok cannot run the validators. Every submission that
lands in `_Collab/10_inbox/` has to be validated, merged, built and committed by Claude,
and *a submission that does not pass is not merged*. This is the half of the campaign that
keeps three platforms producing one reference instead of three.

### If the session has ended and you need a fresh one

Paste this into a new Claude session with the repository folder connected:

---

Continue the Utility Work and Asset Management process specification campaign. The working
repository is at `C:\__Tim Method 2026`, and the public mirror is
`github.com/tbartmann/utility-wam-process-reference`.

Read these first, in this order: `_Collab/00_prompts/SPEC_CAMPAIGN_PROMPT.md`,
`_Collab/00_prompts/ROUND_KICKOFF.md`, `_Collab/SOURCE_AUTHORITY_PACK.md`,
`build/eam/specs/SCHEMA.md` and `build/eam/vocabulary.json`. Then look at
`build/eam/specs/` to see which categories are already specified, and
`_Collab/10_inbox/` to see what is waiting.

This is round `<N>`. Do both jobs:

1. **Merge what has landed.** For each `SPEC_*.json` in the inbox, run
   `python3 validate_spec.py` against it. If it passes, move it into `build/eam/specs/`,
   build its deck with `build_process_spec.py`, and run `validate_models.py` and
   `validate_deck.py`. If it fails, do not merge it — report exactly what failed and what
   the platform has to change. Never fix a submission silently; a correction the author
   does not see is a correction they will make again next round.
2. **Specify your own category** — `<ID> <NAME>` — to the same standard as
   `build/eam/specs/cat-02-plan-design-and-estimate-work.json`, then generate its models,
   build its deck, and run all three validators clean before committing.

The derivation rule governs everything: content enters the reference only if a standard, a
regulation or a recognised industry body says it, and a citation status is never upgraded.
Do not add, move or renumber categories, groups or processes.

Commit with a message that says what changed and why. Then report, in chat: what passed,
what failed and why, which processes were hardest to source, and anything in the Source
Authority Pack that turned out to be wrong or missing.

---

## Round 1 values

| Platform | `<N>` | `<ID> <NAME>` | `<G>` | `<P>` |
|---|---|---|---|---|
| ChatGPT | 1 | 3.0 Plan Resources and Schedule Work | 5 | 21 |
| Grok | 1 | 4.0 Dispatch and Execute Field Work | 6 | 32 |

Claude's round 1 (2.0 Plan, Design and Estimate Work) is complete and merged.

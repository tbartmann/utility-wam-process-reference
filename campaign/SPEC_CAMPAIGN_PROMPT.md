# Process specification campaign — the standing prompt

One category per platform per round. Five rounds. This prompt does not change between
rounds; only the category assignment does.

## The assignment

Category 1.0 is already done and is the **worked example** — read it before starting.

| Round | Claude | ChatGPT | Grok |
|---|---|---|---|
| 1 | **2.0** Plan, Design and Estimate Work | **4.0** Dispatch and Execute Field Work | **3.0** Plan Resources and Schedule Work |
| 2 | **5.0** Close Work, Settle Cost and Update Records | **6.0** Manage Metering and Measurement Operations | **7.0** Manage Vegetation |
| 3 | **8.0** Manage Compliance, Integrity and Safety | **9.0** Manage Outages and Emergencies | **10.0** Serve Customers in the Field |
| 4 | **11.0** Manage Joint Use and Third-Party Attachments | **12.0** Manage Assets and Asset Information | **13.0** Manage Materials and Supply Chain |
| 5 | **14.0** Manage Workforce and Time | **15.0** Manage Performance, Information and Integration | **16.0** Manage Contractors and Partners |

The Asset Lifecycle band (17.0, 18.0, 19.0 — 14 groups, 72 processes) is unassigned and
is not part of rounds 1 to 5. It will be specified after the campaign.

Round 1 was swapped on 2026-08-29: Grok specified 3.0 and ChatGPT takes 4.0. Rounds 2
to 5 are unchanged, and the swap happens to even the totals.

Totals: Claude 148 processes, ChatGPT 134, Grok 134. Each platform gets lifecycle,
specialised and enabling categories, so no single platform's style dominates one band.

## Inputs — read all of these before writing anything

**Public repository: `https://github.com/tbartmann/utility-wam-process-reference`.**
Everything below is in it. The working repository it mirrors is private and contains
client material; you do not need it and should not ask for it.

1. **`_Collab/SOURCE_AUTHORITY_PACK.md`** — the only source list. Binding. Read it first.
2. `build/eam/specs/SCHEMA.md` — the field set and the notation selection rule.
3. `build/eam/specs/cat-01-identify-and-qualify-work-demand.json` — the worked example.
4. `build/eam/specializations/SCHEMA.md` — where observed client material goes instead.
5. `research/Process Modelling Notation - Decision Record.md` — why four layers.
6. `build/eam/model.json` — your category's groups and processes, with their `uid`s.
7. `build/eam/vocabulary.json` — the shared contract. Component codes, CIM classes, the
   full EN 17007 catalogue, decision-variable names, banned terms, the content budget.
   The validators check you against this file, so read it rather than guessing.
8. `build/eam/apqc_pcf_utilities.json` — APQC PCF Utilities v7.2.1, all 2,073 elements.
9. `build/eam/apqc_crosswalk.json` — where this model and APQC disagree, and why.
10. `research/APQC PCF Utilities - Read Against the Model.md` and
    `research/EN 17007 - Read Against the Model.md` — what reading the two frameworks
    against the model actually turned up.

If you cannot reach the repository, say so and ask for these as attachments. Do not
proceed from memory of a different session.

## What changed on 2026-08-29 — read this even if you have seen this prompt before

Round 1 for category 2.0 turned up four problems in the shared contract itself. All are
fixed; you inherit the fixes, but you also need to know they happened.

1. **Two EN 17007 clause numbers in `vocabulary.json` were wrong** — MAN was recorded at
   6.9 and is 6.2; DOC was recorded at 6.10 and is 6.9, which is DTA. Both had already
   reached shipped citations because `validate_spec.py` checked clause numbers for
   level-2 processes only. It now checks both levels. **If you drafted any EN 17007
   citation before this date, re-check it against the vocabulary.**
2. **The EN 17007 catalogue was 11 processes and is now 101.** Cite the level-2 process,
   not the level-1 code, wherever one fits.
3. **APQC PCF Utilities is now in the repository** as JSON, with a hand-authored
   crosswalk. Section A3-bis of the pack has what it found. Eight APQC processes have no
   home in this model.
4. **The deck builder had two slides hard-coded for category 1.0** and would have produced
   a visibly different deck for every other category. Both now derive from the spec JSON.
   Do not edit `build_process_spec.py` for your category — see the trap list below.
5. **The model gained three categories — 17.0, 18.0 and 19.0, the Asset Lifecycle band.**
   APQC and the GFMAM Landscape independently found the same six absences, and the user's
   decision was to close them. **Appended, so nothing renumbered**: 1.0 to 16.0 keep their
   ids, uids and legacy_ids, and your assigned category is untouched. Section A4 of the
   pack has the detail. The one thing that will affect your round directly: a **clearance**
   is produced by **18.4.4**, against a switching plan approved at 18.2.2, under 29 CFR
   1910.269(m). It is not a permit and it does not arrive from nowhere. Cite it.
6. **Every category now carries a `lifecycle` field** in `model.json` saying which asset
   lifecycle stage it serves. Read yours; it tells you which of the two axes your category
   sits on and therefore which framework to test it against.

## The rule that governs everything

**Content enters the reference only if a standard, a regulation or a recognised industry
body says it.** Not from a client programme. Not from a vendor's product design. Not from
your own experience of how utilities usually do it — that is `judgment`, and it must be
labelled as such.

If you find yourself writing something you cannot cite, you have three honest options:
label it `judgment`, leave it out, or record it as a gap. Never a fourth.

**Where a source is paywalled and you have only confirmed the clause number and title,
the status is `clause-verified` and you must NOT reproduce or paraphrase the clause's
content.** Cite it by reference. Every "EN 13306 maintenance types" tree circulating
online is an uncited paraphrase and none of them may be used.

## What to produce

One specification per tier-3 process in your category, keyed by `uid` from `model.json`.
The field set is **EN 17007:2017 cl. 5.2**, which specifies the profile drawn up for each
process. Match the worked example's JSON shape exactly:

```
uid, id, name, group{id,name,uid}
intent            one sentence: the purpose of the process
activities        the tier-4 steps, as a list
trigger           {kind: message|timer|signal|conditional|manual|none, text, cim}
inputs            [{what, party, data}]   party = IEC 61968-6 cl. 4.2 component code
outputs           [{what, party, data}]
systems           [{component, role, service}]
interfaces        [{from, to, payload, verb, pattern}]
roles             [{role, raci}]          product-neutral role names only
data_objects      [CIM class names from IEC 61968-11]
controls          [{kind: regulatory|financial|operational, text}]
measures          [{name, definition, cite}]   from SMRP, EN 15341 or IEEE 1366 only
variants          named cases that run differently — standards-derived only
notation          {class: BPMN|DMN|CMMN|SPEC, why, artifact}
en17007           {process, title, clause}
sources           [{for, cite, status}]   at least three per process
provenance        {basis, primary}
```

**Notation selection — apply per process, do not apply uniformly:**

| Class | Test |
|---|---|
| BPMN | Can you draw the happy path without saying "it depends who is handling it"? |
| DMN | Is the output a value — a classification, priority, due date, route — rather than a state change? |
| CMMN | Would two competent people legitimately sequence it differently? |
| SPEC | Is there an instance with a start and an end? If not, no flow model is owed. |

Expect roughly a third of processes to warrant a model. **Keep CMMN rare** and justify
each one: its spec has not changed since 2016, Camunda 8 dropped it, and choosing it in
practice means choosing Flowable. Category 1.0 came out 11 BPMN, 5 DMN, 2 CMMN.

Do **not** produce the BPMN/DMN/CMMN files. Name the artifact you would build in the
`notation.artifact` field; the merge step builds them so they come out consistent.

## Things that will otherwise go wrong

- **The gas/electric asymmetry is the reverse of the common assumption.** Gas is far more
  heavily regulated on everything a work-management reference is built from. Electric
  distribution has no federal prescriptive interval layer at all, because 16 U.S.C. 824o
  excludes local distribution. Section E of the pack has the capability-by-capability
  table. Do not write "electric is better standardised."
- **Field service management is not a standards domain.** If your category touches
  scheduling, dispatch or mobile execution (3.0, 4.0, 10.0), read section C of the pack
  before you invent citations. The three real anchors are IEC 61968-6 SCHD/FRD,
  EN 15341 O&S indicators, and OSHA — and OSHA's job briefing, information transfer,
  qualified person and minimum approach distance requirements are **dispatch-gating
  process constraints**, not just PPE rules.
- **There is no `WorkOrder` class in CIM.** It is `Work` plus `workOrderNumber`.
  `WorkRequest` is an IEC 61968-6 message payload, not a class.
- **Leak grades are not federal law.** 49 CFR 192.703(c) is the whole federal text.
  ANSI/GPTC Z380.1 is ANSI-accredited consensus, not incorporated by reference. Say both.
- **Part 192 intervals bind twice** — the calendar-year count *and* the not-to-exceed
  month figure. And some are conditional on the prior *outcome*, not just the prior date
  (192.481(d)).
- **APQC's numbering does not imply order**, and flow modelling begins at Level 4 —
  inside a tier-3 process, never above it. APQC is now in the repository as
  `build/eam/apqc_pcf_utilities.json`; read element numbers from it rather than recalling
  them. Only categories 10.0 and 14.0 carry utility content.
- **Do not add groups, add processes, or renumber anything.** If your category is missing
  something APQC or EN 17007 has, that is a finding for the user, not a change for you to
  make. Record it in your spec file's `gaps` array, cite the APQC `pcf_id` or the EN 17007
  code, and report it in chat. Three platforms silently patching the taxonomy in three
  different directions is the failure mode this campaign exists to avoid.
- Observed client practice, if you have any, goes to `build/eam/specializations/`, never
  into the specification. Promotion needs two independent organisations plus a standards
  basis.
- **EN 17007 process codes are not IEC 61968-6 component codes.** They collide by
  spelling and the two namespaces must never be mixed. `DOC`, `SPP`, `HSE`, `MRQ`, `BUD`,
  `RES`, `ACT.2`, `COR.n` and `PRV.n` are EN 17007:2017 clause 6 processes and belong only
  in the `en17007` field. The `party`, `component`, `from` and `to` fields take only the
  sixteen IEC 61968-6:2015 cl. 4.2 codes in `vocabulary.json`. Claude hit this in Round 1
  on four processes; `validate_spec.py` catches it, but only after you have written the
  wrong thing.
- **cl. 4.2 has no component for document management, procurement, or health and safety.**
  There is no honest code for "the document system" or "the procurement system". Put
  documentation and prerequisite ownership on `MAI`, tools and spares on `MM`, clearances
  and isolations on `NO`, and record the absence in `gaps` rather than inventing a code.
- **Do not edit `build_process_spec.py` for your category.** Every slide is generated from
  the spec JSON. If a slide does not fit your category, the builder is wrong for all
  categories, not just yours — fix it generically (column count and text derived from the
  spec) and say so in your report, so the other two platforms inherit the fix. Two slides
  were still hard-coded for category 1.0 when Round 1 started; both are now derived.

## Language

Professional utility-industry voice — the way an experienced operations or IT manager
writes, not the way an AI writes. Concrete nouns, active verbs, no filler. Banned:
leverage (verb), robust, seamless, holistic, delve, journey, empower, cutting-edge,
best-in-class, streamline, unlock, "in today's world". Spell out every acronym at first
use. Sentence case for process and group names, Title Case for categories.

## Check your own work before you submit

You cannot run `validate_spec.py` — you have no Python against this repository, and that
is not a discipline failure, it is a structural limit. **Do not claim a submission passes.**
Say what you checked and what you could not.

But most of what the validator checks is mechanical and you CAN verify it by reading. Walk
this list against your own file before you hand it over. Every item below has actually
rejected a submission.

**Per process — every one, no exceptions:**

- [ ] All ten fields present and non-empty: `intent`, `activities`, `trigger`, `inputs`,
      `outputs`, `systems`, `interfaces`, `roles`, `data_objects`, `controls`, `measures`,
      **`variants`**, `notation`, `sources`, `provenance`. *An entire submission was
      rejected for `variants` missing on all 26 processes.*
- [ ] `id` and `uid` match your assignment pack exactly. Do not invent either.
- [ ] Cardinality inside the content budget in `vocabulary.json` — activities 3–8, inputs
      2–6, outputs 1–5, systems 2–6, roles 2–6, controls 1–4, measures 1–4, variants 0–6,
      sources at least 3.
- [ ] Length caps: `intent` ≤ 140 characters, `notation.why` ≤ 190, each activity ≤ 95,
      `trigger.text` ≤ 135, each control ≤ 300, each measure definition ≤ 150.

**Per citation:**

- [ ] The status is at or below the ceiling in `source_status_ceiling`. Anything ISO, IEC,
      EN, ASTM, ANSI, IEEE, ASME or ASCE is **`clause-verified` at best**. SMRP, AACE, CGA,
      EPRI, API RP, IAM, GPTC and APQC are **`consensus` at best**. Only EN 17007 and the
      GFMAM Landscape support `verified`; only CFR, U.S.C., MUTCD and USACE support
      `regulation`.
- [ ] Nothing paraphrases the body of a `clause-verified` source. Clause number and title
      only.
- [ ] Measures cite SMRP, EN 15341 or IEEE 1366 and nothing else.

**Per field:**

- [ ] `party`, `component`, `from` and `to` carry only the sixteen IEC 61968-6 cl. 4.2
      codes. EN 17007 codes — DOC, SPP, HSE, TOL, MRQ, BUD, RES — belong only in
      `en17007`.
- [ ] `en17007.process`, `.title` and `.clause` match `vocabulary.json` exactly. Two clause
      numbers in that file were wrong until 2026-08-29; use the file, not your memory.
- [ ] No banned term and no vendor or client name anywhere.

**Then say, in your reply:** which items you checked, which you could not, and where you
are unsure. A submission that names its own weak points is worth more than one that claims
to be clean.

## Output contract

ONE file: `SPEC_<category>_<Platform>.json`, in
`02 Industry Specialization/Utilities/_Collab/10_inbox/`.

Wrap the specifications in this envelope:

```
{
  "category": {"uid":…, "id":"N.0", "name":…, "band":…},
  "platform": "<ChatGPT|Grok|Claude>",
  "model": "<exact model name/version>",
  "round": <n>,
  "date": "YYYY-MM-DD",
  "derivation": "STANDARDS-DERIVED. …",
  "field_set": "EN 17007:2017 cl. 5.2 …",
  "gaps": [ "things you could not source, stated plainly" ],
  "processes": [ … one object per tier-3 process … ]
}
```

Also return, in chat and not in the file, a short note covering: which processes you
found hardest to source and why; anything in the Source Authority Pack that turned out
to be wrong or missing; and any place your category's existing group boundaries look
wrong against EN 17007 or APQC PCF Utilities. That last one is the point of doing this —
the campaign is also a test of the taxonomy.

## Repository operating rules (binding)

1. Operate **read-only** on everything except your own output file. Do not move, rename,
   delete or reorganise anything, and do not suggest doing so.
2. Your entire output is ONE new file in `_Collab/10_inbox/`. If you cannot write to the
   repository, return the content in chat and Tim will place it.
3. Do not edit `model.json`, the build scripts, the specs, the models, or any deck.
   Propose changes as notes in your chat response; the merge step applies them.
4. Do not commit, push, branch, tag or rewrite history. Decline any tooling offer to
   create a pull request.
5. Generated files under `_Collab/knowledge-pack/` are derived from `model.json` — never
   edit them, and never treat a difference between them and the decks as an error to fix.
6. If something is missing, contradictory or broken, report it under `gaps` — do not
   attempt a repair.
7. Do not add values to `build/eam/vocabulary.json`. It is the shared contract; changing
   it unilaterally is how three platforms stop being comparable.

# Process specification schema

One specification per tier-3 process. Keyed by `uid`, the permanent element id from
`model.json` — never by the dotted id, which is positional and has already changed once.

## The rule that governs this layer

**The reference is derived from standards and industry-body consensus only.** Every
field in every specification carries a citation to a named standard, a regulation, or
an ANSI-accredited or equivalent industry body. Nothing in this layer is generalised
from a single utility's implementation, a vendor's product design, or a client
programme's design documents.

Observed client and programme material is real evidence and worth keeping, but it
belongs in `../specializations/`, which overlays the reference and is never merged into
it. See `../specializations/SCHEMA.md`. A specialization may contradict the reference;
that is the point of having two layers.

## Field set

The field set is EN 17007's, not one of ours. **EN 17007:2017 clause 5.2** specifies
the profile drawn up for each process, verbatim:

> "A profile is drawn up for each level 2 process. It includes: — the name of the
> process; — the purpose(s) of the process...; — the activities that comprise the
> process...; — the input data and products which are needed to realize the process...;
> — the output data and products which are created or modified by the process...; —
> ...the stakeholders...; — the interfaces with the other processes...; — the
> constraints related to realization of the process...; — Elements to define indicators
> related to the process."

ISO 9001:2015 clause 4.4.1 requires the same determinations at management-system level
— inputs and outputs a), sequence b), criteria and measures c), resources d),
responsibilities e), risk f), evaluation g). The two agree; EN 17007 is the
domain-specific one and is cited first.

| Field | EN 17007 cl. 5.2 element | ISO 9001 4.4.1 | Notes |
|---|---|---|---|
| `uid` | — | — | Permanent element id. The join to `model.json`. |
| `intent` | purpose | — | One sentence. |
| `activities` | activities | b) | Tier-4 steps. This is where BPMN begins, not above. |
| `trigger` | (input, event) | b) | `kind`, `text`, `cim` where IEC 61968-6 applies. |
| `inputs` | input data and products | a) | `what`, `party` (IEC 61968-6 cl. 4.2 component), `data` (CIM class). |
| `outputs` | output data and products | a) | `what`, `party`, `data`. |
| `systems` | (input data suppliers) | d) | Component code, role, ArchiMate application service. |
| `interfaces` | interfaces with other processes | a) d) | `from`, `to`, `payload`, `verb`, `pattern`. |
| `roles` | stakeholders | e) | Product-neutral role names with a RACI position. |
| `data_objects` | — | a) | CIM classes from IEC 61968-11. |
| `controls` | constraints | f) | Regulatory, financial and operational. EN 17007 calls these constraints. |
| `measures` | elements to define indicators | c) g) | Cited to EN 15341 and SMRP, not invented. |
| `variants` | — | b) | Named cases that run differently. Standards-derived only. |
| `notation` | — | b) | `class`, `why`, `artifact`. |

### Artifact granularity — BPMN at the group, DMN and CMMN at the process

A behaviour model exists to show a **sequence across processes**: how 2.1.1 flows into
2.1.2 and where it branches. One BPMN file per tier-3 process shows thirty disconnected
fragments and loses the only thing BPMN is for.

So:

- **BPMN** — one file per **process group**, named `<group>-<kebab-name>.bpmn`, covering
  every BPMN process in that group. `2.1-engineer-and-design-work.bpmn` carries 2.1.1
  through 2.1.4. A group with two BPMN files is an error.
- **DMN** — one file per **process**, named `<process>-<kebab-name>.dmn`. A determination
  is its own thing and is called from the group's BPMN as a business rule task.
  `2.2.5-capitalisation-determination.dmn`.
- **CMMN** — one file per **process**, named `<process>-<kebab-name>.cmmn`, for the same
  reason. `2.4.4-scope-change.cmmn`.
- **SPEC** — no artifact. `null`.

The ratio to expect is roughly one artifact per two processes. The five merged categories
run 18 processes to 7 models, 26 to 11, 21 to 9, 20 to 6 and 22 to 11. Thirty models for
thirty-two processes means the group boundaries were not used.
| `en17007` | — | — | The EN 17007 process this corresponds to. |
| `sources` | — | — | Per-field citations with a verification status. |
| `provenance` | — | — | `grade`, `corr`, `warrant` — same scheme as `eam/provenance.py`. |

## Source verification status

Every entry in `sources` carries a `status`, because most of this material is paywalled
and the difference matters:

| Status | Meaning |
|---|---|
| `verified` | The cited text was read verbatim from official or issuing-body text. |
| `clause-verified` | Clause number and title confirmed from official text; the clause body is paywalled and was not read. |
| `consensus` | Published guidance from a recognised industry body, not a standard, and not law. |
| `regulation` | Verbatim from the current eCFR or equivalent primary regulatory text. |
| `judgment` | Professional inference. Not attributed to any source. |

Nothing is cited as `verified` that was read only in paraphrase. Where a widely
repeated "fact" could not be traced to primary text, it is left out rather than
softened — see the decision record's list of things not to take on trust.

Two of those claims are checked against the citation string itself, because a status the
string cannot support is worth nothing:

* **`clause-verified` must name a clause.** The status means the clause number and title
  were confirmed. A citation that names only the standard - `IEEE 1366-2022`,
  `IEC 61968-9:2024 Ed. 3` - has confirmed nothing about a clause, and its honest status
  is `consensus`: the body publishes this standard, and that is the whole claim. A
  locator may be a clause, an Annex, a Table, a CFR section, a NESC Rule, a named UML
  package in IEC 61968-11, a numbered GFMAM subject, a numbered CGA practice or a FERC
  account. Name the clause or drop the status; never invent the number.
* **An absence is a `judgment`.** A citation that opens by asserting no document requires
  a thing is an inference, whatever authoritative document is named beside it. If a
  document does support the absence - a scope clause, an applicability section,
  16 U.S.C. 824o excluding local distribution - cite that document and let the clause
  make the claim, and keep the conclusion drawn from it as a separate `judgment` entry.

## Notation selection rule

| Class | When | Test |
|---|---|---|
| BPMN | The sequence is known before the instance starts, and repeats. | Can you draw the happy path without saying "it depends who is handling it"? |
| DMN | The work is a determination from inputs against rules. | Is the output a value — a classification, priority, due date, route — rather than a state change? |
| CMMN | A skilled person chooses what to do next from available actions. | Would two competent people legitimately handle it in a different order? |
| SPEC | A standing capability with no instance boundary, **or** a determination whose rule cannot be stated from a source. | Is there an instance with a start and an end? If not, specification only. If there is, but writing the DMN would mean inventing the rule, specification only — and say which of the two reasons applies. |

EN 17007 Table 2 states its own notation is BPMN 2.0, which is the standards-body
precedent for drawing maintenance processes in BPMN at this level.

The second SPEC case exists because the derivation rule outranks the notation rule. A
forecast, a safety-stock level and a criticality class are all determinations and all
pass the DMN test on shape — but no source in the pack states the arithmetic, and a DMN
decision table whose rules were invented would be worse than no model. Category 3.0's
scenario simulation is already in the reference on this basis. What the rule requires is
that `notation.why` says which case applies, because "standing" and "unsourceable" are
different claims and only one of them is about the shape of the work.

## Vocabulary sources

- **Process spine** — EN 17007:2017, CEN/TC 319. Sixteen level-1 processes; the
  demand-to-release chain is PRV.1, PRV.2 (planned demand), COR.1 "Classify the actual
  events", COR.2 "Diagnose the state of the items in question", ACT.1 "Rank the events",
  ACT.2 to ACT.5 (prepare, sequence, schedule, release). Every tier-3 process here maps
  to one of these in its `en17007` field.
- **Maintenance vocabulary and work types** — EN 13306:2017 cl. 7 "Maintenance types";
  Annex E "Criticality matrix". ISO 14224:2016 cl. 9.6.2 "Maintenance categories".
- **Work order definition and data** — EN 15341:2019+A1:2022 cl. 3.8 and EN 13460:2009
  cl. 3.8 both define it; EN 13460 Annex B is "Work order information items".
- **Indicators** — EN 15341:2019+A1:2022 cl. 12, indicators O&S9 to O&S22 "Planning and
  Control". SMRP Best Practices Pillar 5 "Work Management" metric numbers. SMRP and
  EFNMS publish a harmonised list, which is what lets one measure set span both.
- **System components** — IEC 61968-6:2015 cl. 4.2 reference components: `GINV`, `MAI`,
  `CON`, `DGN`, `SCHD`, `FRD`, `AM`, `NO`, `SIM`, `NE`, `TCM`, `MR&C`, `CS`, `HR`, `MM`,
  `FIN`. Product-neutral by construction.
- **Messages and verbs** — IEC 61968-6 cl. 5.3 to 5.5 payloads (`WorkRequest`,
  `ServiceOrder`, `MaintenanceOrder`) and Annex A verbs.
- **Data objects** — IEC 61968-11 CIM `Work` package. There is no `WorkOrder` class —
  use `Work` plus the `workOrderNumber` attribute.
- **Gas compliance intervals** — 49 CFR Part 192, current eCFR text.
- **Leak grading** — ANSI/GPTC Z380.1, Guide Material Appendix G-192-11. ANSI-accredited
  consensus, **not incorporated by reference into Part 192**; the federal text is
  § 192.703(c) alone. Binding only where a state adopts it. Say both.
- **Electric reliability measures** — IEEE 1366.
- **Locate requests** — CGA Best Practices.

## Known vocabulary gaps, recorded not hidden

- IEC 61968 is scoped to **electric** utilities. Gas distribution work management has no
  CIM equivalent; gas borrows electric vocabulary here.
- **Electric distribution inspection has no federal prescriptive interval layer.** It is
  state by state. Where an interval is needed, the reference names the state exemplar
  rather than implying a national rule.
- **There is no consensus definition, spanning gas and electric, of what a work request
  must contain.** IEC 61968-6 is the closest and is electric-only.
- EN 13306 cl. 7's maintenance-type definitions and EN 15341's individual O&S indicator
  names are paywalled. They are cited as `clause-verified` and their content is not
  reproduced or paraphrased.

## Files

    specs/cat-01-identify-and-qualify-work-demand.json
    ../models/<id>-<slug>.bpmn | .dmn | .cmmn      OMG-valid, no vendor attributes
    ../specializations/<client>/                   observed overlays, never merged

## Optional fields: structure built now, content researched later

Five things four operators showed the reference cannot express. The fields exist so the
work can be done; none is populated, and absent is a legal state. The validator
shape-checks them only when present, because a half-filled field that looks researched is
worse than an empty one.

| Field | On | Holds |
|---|---|---|
| `handoffs` | process | `to`, `what`, `trigger` — which process this one hands to, and what passes |
| `evidence` | process | `record`, `retention`, `authority_ref` — the compliance record produced or updated |
| `controls[].authority` | control | who imposes it: `federal-rule`, `federal-statute`, `state-code`, `commission-order`, `consensus-standard`, `commitment`, `operator-set` |
| `controls[].jurisdiction` | control | `federal`, or a two-letter state. Required when the authority is a state code or a commission order |
| `vocabularies` | process | names of the controlled value sets this process depends on |

### Why `handoffs` exists when `interfaces` already does

EN 17007 cl. 5.2 asks for "the interfaces with the **other processes**". The `interfaces`
field is mapped to that element and populated with something else: system-to-system message
flows between landscape components — `{"from": "MAI", "to": "FRD", "payload":
"WorkRequest"}`. Those are IEC 61968-6 component interfaces, and they are worth having, but
they are not what the cited clause asks for.

So the slot for process handoffs was not empty, it was occupied. `handoffs` restores the
EN 17007 element and leaves `interfaces` doing the landscape job it actually does.

This matters because the seams are where integrated work fails. An operator's own test
scenarios carried a column for exactly this — "other process designs touched" — and it was
answered "N/A" in twenty-one of twenty-three rows. An optional column gets skipped; a field
with a shape check does not.

### Why `evidence` is a field and not a note

55 regulatory controls across the library require a record or evidence, and the data layer
offers 17 CIM classes, every one of them work, asset or resource centric. `WorkActivityRecord`
is the closest and it is bound to a work activity, so it dies with the order.

The reference states the problem in its own words at 1.2.2: "each report of a hazard needs
its own evidence of investigation and response **even where the resulting work is merged**".
A work-centric model loses one of two merged reports. `evidence` is where the thing that
survives the merge is named.

### Why authority is separate from the clause

The library cites 298 federal instruments and four state ones. Above the federal floor is
exactly where operators in different states differ, and a clause alone cannot say who
imposes it — 18 CFR 101 is the federal uniform system of accounts, and a state commission
adopting that same text for intrastate ratemaking is a different authority applying
identical wording.

`commitment` and `operator-set` matter more than their counts suggest. A rate case or
settlement commitment binds as firmly as a rule and appears in no code book. And
`operator-set` is the honest label for an interval nobody imposed — the case where a
client's difference is a free choice rather than a deficiency.

## Declaring what is not established

The reference is built at varying levels of completeness on purpose. It will never be
finished: it accumulates from standards research, client input and recall, and each pass
knows more than the last. So a process may declare fields it cannot yet establish:

```json
"not_established": {
  "measures": "EN 15341 individual indicator names are paywalled; no cited indicator
               exists for this process yet."
}
```

A declared field may then be empty, and the specification validates. The cardinality
budgets skip it too.

**Why this is allowed at all.** Requiring every field to be non-empty does not produce
completeness. It produces **fabrication**. An author with no evidence and a validator
demanding content writes judgment, and the judgment reads exactly like a fact once it is
on the page — same font, same field, same slide. Every instance of that defect found in
this library began there: four roles on all forty-nine processes because the field could
not be empty; one rationale repeated on a hundred and seventy-two; a notation reason
copied because something had to be written.

A declared unknown costs a sentence of reasoning, and it is cheaper than the fabrication
it replaces in every direction: it is honest, it is countable, and it hands the next
research pass a worklist instead of five hundred and three processes to re-read.

**What it is not.** It is not a licence to leave work undone quietly. The reason is
mandatory, it is reported on every run, and a declaration that names a field nobody
recognises is an error. The counts appear at the end of each validation:

```
completeness: 359 field(s) established, 1 declared not established (measures 1)
optional carried: handoffs 1, evidence 1
```

**Where it sits relative to citation status.** They are different axes and both are needed.
Citation status says how well a stated fact is evidenced, and may only ever be lowered.
`not_established` says no fact is stated yet, and is expected to be removed as research
arrives. A field can be established and weakly cited; it cannot be both established and
not established.


## The envelope `gaps` array, and why it is not `not_established`

Every envelope carries a `gaps` array: prose statements about what this category could
not source. There are 179 of them. They are NOT candidates for `not_established`, and the
distinction matters enough to write down, because it was tested and it failed.

`not_established` says no fact is stated yet, so the field may be empty. Every field the
179 statements name is populated, and populated correctly — the absence of an authority
is already recorded on the axis built for it: citation status `judgment`, notation class
`SPEC`, or a control whose text says in words that the operator must set the rule.
Converting them would mean DELETING established content to make room for a declaration
saying less than the content did. A field can be established and weakly cited; it cannot
be both established and not established.

What the array needed was not a different field but a TYPE. Flattened into one array it
mixes at least four kinds that want four different responses — an instrument that exists
and is not held, an instrument that exists and does not bind, a rule that belongs to a
State, a boundary held on purpose, and an internal inconsistency somebody still has to
decide — and the ones that are actionable hide among the ones that are not.
`eam/gaps/classify_gaps.py` types them and writes `eam/gaps/REPORT.md`. It is derived:
the envelope prose stays the record, statements are keyed by a hash of their own text so
a rewording shows up as a new statement, and twelve of the nineteen envelopes are other
platforms' submissions and are never edited.

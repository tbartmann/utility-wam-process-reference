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

## Notation selection rule

| Class | When | Test |
|---|---|---|
| BPMN | The sequence is known before the instance starts, and repeats. | Can you draw the happy path without saying "it depends who is handling it"? |
| DMN | The work is a determination from inputs against rules. | Is the output a value — a classification, priority, due date, route — rather than a state change? |
| CMMN | A skilled person chooses what to do next from available actions. | Would two competent people legitimately handle it in a different order? |
| SPEC | A standing capability with no instance boundary. | Is there an instance with a start and an end? If not, specification only. |

EN 17007 Table 2 states its own notation is BPMN 2.0, which is the standards-body
precedent for drawing maintenance processes in BPMN at this level.

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

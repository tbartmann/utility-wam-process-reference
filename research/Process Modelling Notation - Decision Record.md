# Process modelling notation: decision record

Decision record, 2026-08-28. The question: to model each process in the reference —
how it is done, what the inputs are, which systems supply them, and everything else
about it — should we use BPMN, CMMN or DMN?

**Decision: none of them on their own, and not as a choice between them. Four layers,
each with a different standard, because the four things being modelled are different
things.** BPMN, CMMN and DMN are all layer 2. The thing described in the question —
inputs, supplying systems, everything about the process — is layer 1, and no OMG
notation covers it.

---

## The four layers

| Layer | What it holds | Standard | Where it lives |
|---|---|---|---|
| **1. Specification** | Trigger, inputs, outputs, supplying systems, data objects, roles, controls, measures, variants | ISO 9001 cl. 4.4; ASQ SIPOC+CM for shape | `build/eam/specs/*.json`, keyed by `uid` |
| **2. Behaviour** | How the work actually runs | BPMN 2.0 / CMMN 1.1 / DMN 1.5 — chosen per process, see below | `build/eam/models/*.bpmn`, `.dmn`, `.cmmn` |
| **3. Data** | The nouns the flow moves | IEC 61968-11 CIM classes; IEC 61968-6 message payloads and verbs | `meta.data_vocabulary` in the spec |
| **4. Landscape** | Which system supplies which input | ArchiMate 3.2 relationship pattern; IEC 61968-6 cl. 4.2 component names | `systems` and `interfaces` in the spec |

Layer 1 is the one that makes the reference useful for scoping, requirements and
capability work, and it is the one nobody publishes. Layers 2 to 4 are what make it
executable later.

---

## Correction, 2026-08-28: the field set is EN 17007's, not ours

This record originally justified the specification layer from ISO 9001 cl. 4.4 and gave
its field set the shape of ASQ's SIPOC+CM. That was defensible but it was not the best
available answer, and it missed the standard that governs this directly.

**EN 17007:2017, *Maintenance process and associated indicators*** (CEN/TC 319, October
2017) is a maintenance **process reference model**. Its scope, verbatim: "This European
Standard provides a generic description of the maintenance process. It specifies the
characteristics of all the processes, parts of maintenance process, and establishes a
maintenance model to gives guidelines for defining indicators." Clause 5.2 specifies the
profile drawn up for each process, verbatim: "the name of the process; the purpose(s) of
the process...; the activities that comprise the process...; the input data and products
which are needed to realize the process...; the output data and products which are
created or modified by the process...; the stakeholders...; the interfaces with the other
processes...; the constraints related to realization of the process...; Elements to
define indicators related to the process."

That is the field set, from a standards body, for this exact purpose. It is now used
directly. ISO 9001 cl. 4.4.1 is retained as corroboration because it requires the same
determinations at management-system level, and because it is the clause an auditor will
know. SIPOC is dropped — it has no standards backing and no reliable attribution, and it
was only ever a shape.

Two further things EN 17007 settles. Its Table 2 records that its own notation is
**BPMN 2.0**, which is standards-body precedent for the layer-2 choice below. And clause
5.4 of EN 15341 defers to EN 17007 for process definition, so the process standard and
the KPI standard are designed to be used together — which is why the indicator fields
here cite EN 15341 cl. 12 rather than inventing measures.

**The demand chain in EN 17007's own vocabulary**, which category 1.0 now maps to:
PRV.1 "Characterize the undesirable events" and PRV.2 "Use and update the Maintenance
Plans" generate planned demand; COR.1 "Classify the actual events" takes unplanned
demand; COR.2 "Diagnose the state of the items in question"; ACT.1 "Rank the events";
ACT.2 to ACT.5 prepare, sequence, schedule and release. Note the standard says *events*,
not requests.

## The derivation rule

**Content enters the reference only if a standard, a regulation or a recognised industry
body says it.** Observed client and programme material is real evidence and is kept, but
in a specialization layer that overlays the reference and is never merged into it.
Promotion into the reference requires two independent organisations plus a standards
basis. One programme is never enough: generalising one utility's implementation puts
that utility's choices, and its vendors' constraints, into a document claiming to speak
for the industry — and once paraphrased into neutral language it can no longer be
identified or challenged. See `build/eam/specializations/SCHEMA.md`.

## Why the specification layer is not optional, and not BPMN

**ISO 9001:2015 clause 4.4.1 requires an organisation to determine, for each process:**

> a) the inputs required and the outputs expected from these processes;
> b) the sequence and interaction of these processes;
> c) the criteria and methods (including monitoring, measurements and related
> performance indicators) needed to ensure the effective operation and control of these
> processes;
> d) the resources needed for these processes and ensure their availability;
> e) assign the responsibilities and authorities for these processes;
> f) address the risks and opportunities...;
> g) evaluate these processes...;
> h) improve the processes...
> [source: ISO 9001:2015 cl. 4.4.1]

A BPMN diagram evidences (b) and nothing else. Everything in the question — inputs,
supplying systems, all of it — is (a), (c), (d) and (e). That is the specification
layer, and ISO does not prescribe a notation for it: clause 4.4.2 only requires
documented information "to the extent necessary". So the field set is ours to design,
and it should be designed against a) to h).

Note the standard is being reissued: ISO/TC 176/SC 2 announced on 7 August 2026 that
the FDIS passed, with the sixth edition due 16 September 2026. Independent clause
review reports 4.4 taking minor language changes and no new requirements. Cite the
clause, not the year, and re-check on publication. [source: ISO/TC 176/SC 2]

For the shape of the field set, ASQ's **SIPOC+CM** is the closest citable convention —
suppliers, inputs, process, outputs, customers, plus **C**onstraints and **M**easures.
[source: ASQ] Two honest caveats: no standards body defines SIPOC and there is no
reliable attribution of its origin, and the **turtle diagram** has no standards backing
at all — the word "turtle" does not appear in the IATF 16949 FAQ. Use the turtle's
question set as an interview checklist; anchor the model's authority to ISO 9001 4.4.

---

## Why a taxonomy cannot be drawn in BPMN

The reference is a three-level taxonomy: category, process group, process. None of
those three levels is a BPMN process, and drawing them as one would produce diagrams
that look like BPMN and mean nothing in it.

APQC, whose numbering convention this reference follows, is explicit that its hierarchy
is an unordered decomposition:

> "Although process elements are numbered ascendingly, it is important to understand
> this does not imply that process elements occur in a certain order."
> [source: APQC, Understanding the Elements of the PCF]

> "a process group is defined by the processes underneath it; a process is defined by
> the activities underneath it" [source: APQC]

And APQC's levels tell us exactly where flow begins: Level 1 Category, Level 2 Process
Group, Level 3 Process, **Level 4 Activity — "a key step performed to execute a
process"**, Level 5 Task. [source: APQC] Activities are ordered steps. Processes are not.

Bruce Silver makes the same point from the BPMN side: high-level framework entries are
"indistinguishable from functions or capabilities. **They are not really processes**",
where a real process activity is one "performed repeatedly in the course of business,
with each instance having a well-defined start and end". [source: Silver, *BPMN and
Business Process Architecture*, 2016-12-29]

**Consequence for us.** One specification per Level 3 process — the 434 we already have.
BPMN starts at Level 4, inside a process, and is written only where it earns its place.

A naming hazard to settle now: Silver's BPMN "levels" (Descriptive, Analytic,
Executable) are BPMN subclasses and have nothing to do with taxonomy levels 1/2/3. This
reference says **tier** for the taxonomy and **BPMN class** for Silver's, always.

---

## Layer 2: which notation, per process

The three OMG standards are complementary by their own specifications, not alternatives.

**CMMN 1.1, clause 1 Scope**, on itself versus BPMN:

> "This specification is intended to be consistent with and complementary to BPMN."
>
> "[BPMN] processes are described as the predefined sequences of activities with
> decisions (gateways)... These models are effective for **predefined, fully specified,
> repeatable business processes**."
>
> "there has been discussion of the need to model activities that are **not so
> predefined and repeatable, but instead depend on evolving circumstances and ad hoc
> decisions by knowledge workers** regarding a particular situation, a case."
> [source: CMMN 1.1, formal/2016-12-01]

CMMN's own list of intended applications names "licensing and permitting" and
"maintenance and repair of machines and equipment" — this industry, from the spec.

**DMN 1.5, clause 5**, on why decision logic leaves the process model:

> "decision-making has an internal structure which is not conveniently captured in
> either of these modeling perspectives... DMN will provide a third perspective — the
> Decision Requirements Diagram — **forming a bridge between business process models and
> decision logic models**... complements a business process model by specifying in
> detail the decision-making carried out in process tasks."
> [source: DMN 1.5, formal/24-01-01]

DMN's own worked example shows the pattern: decision points become business rule tasks
calling decision services, and gateways route on the **returned value** rather than
embedding the logic. [source: DMN 1.5 cl. 11.1.2] Note that the popular line about not
modelling decisions as "gateway spaghetti" is practitioner framing, not spec text — do
not attribute it to OMG.

**The selection rule this reference adopts:**

| Use | When | Test |
|---|---|---|
| **BPMN 2.0** | The sequence is known before the instance starts and repeats | Can you draw the happy path without saying "it depends who is handling it"? |
| **DMN 1.5** | The work is a determination from inputs against rules | Is the output a value — a classification, a priority, a due date, a route — rather than a state change? |
| **CMMN 1.1** | A skilled person chooses what to do next from available actions | Would two competent people legitimately handle it in a different order? |
| **None** | The process is a standing capability, or evidence of it | Is there an instance with a start and an end? If not, specification only. |

Most of the reference is BPMN or specification-only. DMN is concentrated in
classification, prioritisation, compliance intervals and sourcing rules. CMMN is rare
and should stay rare — see the risk below.

---

## Flowable: confirmed as the target, with three warnings

Flowable is the right engine choice. It is the leading actively-developed open-source
engine executing all three standards on one platform, and current: **8.0.0, released
2026-02-27**. Camunda 7 supported CMMN; Camunda 8 does not, and Camunda said so in 2020
— "we decided that we would not be adding any more CMMN features... The future of
Camunda right now is with BPMN and DMN". [source: Camunda blog, 2020-08-20]

Three warnings that belong in the plan, not discovered later.

**1. Flowable has no FEEL, so DMN portability is a fiction.** DMN defines conformance
levels; level 2 requires S-FEEL and level 3 full FEEL. Flowable's DMN engine uses JUEL
instead — its own documentation says "we do not supported this part of the
specification. Within Flowable DMN, we use JUEL as the expression language." A `.dmn`
authored for Flowable will not run on Camunda, Trisotech or Drools, and theirs will not
run on Flowable. The XML structure is portable; the expressions are not. If
vendor-neutrality is the selling point, say plainly that it holds at the *structure*
level.

**2. Standard XML deploys, but inert.** Flowable reads OMG-valid BPMN, CMMN and DMN.
Every behavioural binding, though, is a vendor attribute: `flowable:class`,
`flowable:delegateExpression`, `flowable:assignee`, `flowable:candidateGroups`, and DMN
invoked as `<serviceTask flowable:type="dmn">` rather than BPMN's native
`businessRuleTask`. Flowable also adds non-standard CMMN constructs — its docs concede
the Completion Neutral Rule "is not a CMMN 1.1 Standard, but a Flowable-specific
addition". **So the reference model keeps two things apart: OMG-valid files that are the
published reference, and a Flowable binding layer applied on top.** Never let vendor
attributes leak into the reference files.

**3. CMMN is a niche standard on a frozen spec.** CMMN 1.1 has not changed since
December 2016. Camunda 8 dropped it, Camunda's Modeler disables the CMMN editor by
default, the Operaton fork is openly debating removal, and Freund & Rücker removed CMMN
from the next edition of *Real-Life BPMN*. A 2026 peer-reviewed paper opens with "its
adoption remains limited due to conceptual and visual shortcomings". [source: Bule &
Polančič, *Systems* 14(2):180, 2026] It is not dead — a 2021 study found modellers
positive about it, and Flowable is still investing in 8.0.0 — but choosing CMMN in
practice now means choosing Flowable. For a utility with a fifteen-year platform
horizon that is a real consequence. **Use CMMN only where BPMN genuinely cannot express
the work, document why each time, and expect fewer than ten of the 434 processes to
qualify.**

Also worth recording: Flowable's published documentation is stale on version facts —
its DMN page is titled "DMN 1.1", its standards page says 1.2, and the 8.0.0 source
tree uses the DMN 1.3 namespace. Read the source, not the docs.

Current OMG versions as of today: **BPMN 2.0.2** (formal/2013-12-09, also ISO/IEC
19510:2013, confirmed current in 2022; a 2.1 revision task force is chartered but has
published nothing in twelve years); **CMMN 1.1** (formal/2016-12-01); **DMN 1.5**
(formal/24-01-01, with 1.6 and 1.7 in beta — OMG's own note says the formal version "is
the version that should be followed for compliance").

---

## Layers 3 and 4: the vocabulary problem, and the answer

If the reference is to generate a generic solution, the flows are worthless without
shared nouns and a shared idea of which system supplies what.

**Data objects: IEC 61968-11.** The CIM `Work` package under IEC 61968 gives
`BaseWork` ("common representation for work and work tasks"), `Work` ("document used to
request, initiate, track and record work"), `WorkTask` ("a task within a set of work"),
plus `WorkActivityRecord`, `WorkLocation`, `MaterialItem`, `Tool`, `Vehicle` and the
`WorkKind` / `WorkStatusKind` / `WorkTaskKind` enumerations.

An honest correction to a common assumption: **there is no `WorkOrder` class and no
`WorkRequest` class in the CIM UML.** "Work order" survives as an attribute,
`Work.workOrderNumber`. `WorkRequest` exists only as a message payload name in
IEC 61968-6. Say `Work` + `workOrderNumber`, and cite `WorkRequest` as a message.

**Triggers and messages: IEC 61968-6:2015**, *Interfaces for maintenance and
construction*. It defines three payloads — **WorkRequest**, **ServiceOrder** and
**MaintenanceOrder** — and Annex A gives the verb set (create, change, cancel, close,
get, reply) that forms the trigger vocabulary. Its clause 4.1 states the linkage
outright: message fields are "copied from the information model classes in
IEC 61968-11".

**Supplying systems: IEC 61968-6 clause 4.2** names the reference components, which is
exactly the product-neutral system vocabulary this reference needs — GINV geographical
inventory, MAI maintenance and inspection, CON construction, DGN design, SCHD work
scheduling and dispatching, FRD field recording, AM asset management, NO network
operations, TCM trouble call management, MR&C meter read and control, CS customer
service, plus HR, materials management and finance. Its Figure 2 numbers the data flows
between them — request for service, request for planned maintenance, request for
unplanned work, follow-up work, work order, crew composition, actual labour cost.

**The relationship pattern: ArchiMate 3.2** (The Open Group, October 2022). The question
"which systems supply the inputs" is answered by:

    Application Component --realization--> Application Service
    Application Service   --serving-----> Business Process
    Business Process      --access------> Business Object     (read / write / read-write)
    Business Role         --assignment--> Business Process

Two refinements adopted here: bind an **Application Service** to the process rather than
an Application Component, so the model survives a system replacement; and use the
`Access` direction to distinguish an input from an output on the same object.

**Caveats.** IEC 61968-6 is still edition 1.0 from 2015 and says itself that
construction functions "will be included in future editions". And the whole 61968 series
is scoped to electric utilities — **for gas distribution work management there is no IEC
CIM equivalent**, so gas borrows electric vocabulary here. That gap is recorded, not
hidden. MultiSpeak (NRECA) may be closer to installed integration at co-ops.

---

## What already exists, and what does not

Worth knowing before claiming novelty.

- **APQC PCF Utilities 8.0** (Excel, 20 August 2026) is the best-maintained utility
  taxonomy. APQC also publishes a **Members' BPMN version — but pinned at 6.1.0** and
  behind membership.
- **Oracle Utilities Reference Models** are public and free, and 5.8 *Manage Work and
  Projects* is directly on this subject (Manage Work Request, Manage Work Orders, Manage
  Approvals, Assign and Schedule Work, Report Time). But they ship as **Visio plus Word**,
  not BPMN; they are **product-coupled** — the narratives cite Oracle algorithm codes such
  as `W1-DFWRASLOC` and business object `W1-WorkRequest`; and the WAM models were last
  updated in 2016. Their document structure is a useful template. What they lack is
  exactly our layer 1: no trigger, no input inventory, no supplying-systems list, no
  controls, no measures.
- **EPRI** publishes a utility *capability* model, not a process model.
- **TM Forum TR239** maps utilities onto eTOM but is pinned to Frameworx R14.5.1 (2014)
  and is an exploratory report.
- **IEC 61968 and MultiSpeak** give vocabulary and messages, no process flow.

**No open, vendor-neutral, standards-body-published BPMN reference process model exists
for gas and electric distribution.** Nothing found publishes trigger plus inputs plus
outputs plus supplying systems plus data objects plus controls plus measures for this
industry. That gap is the reason this layer is worth building.

---

## The construction we adopt

    Taxonomy tiers 1-3        this reference's 16 / 89 / 434, numbering APQC-style
      └─ one specification per tier-3 process    ISO 9001 4.4 field set, keyed by uid
           ├─ data objects                       IEC 61968-11 CIM classes
           ├─ messages and triggers              IEC 61968-6 payloads and verbs
           ├─ supplying systems                  IEC 61968-6 cl. 4.2 components,
           │                                     ArchiMate serving/access relationships
           └─ behaviour, tier 4                  BPMN 2.0 | DMN 1.5 | CMMN 1.1 | none
                └─ Flowable binding layer        vendor attributes, kept separate

Specifications are keyed by `uid`, not by dotted id, so the 2026-08-28 renumbering
cannot happen to them again.

## Consequences

- The reference gains a layer nobody else publishes, and it is the layer that makes it
  usable for requirements and scoping rather than only for orientation.
- Coverage will be uneven for a long time, and that is correct. Specify all 434;
  model behaviour only where it earns its place. A fully BPMN-modelled 434-process
  reference is a multi-year effort and most of it would be waste.
- Vendor-neutrality holds at the structure level and not at the expression level. Say so.
- Committing to CMMN concentrates risk on Flowable. Keep the count low and justified.
- Gas work management has no CIM equivalent; the data layer is electric vocabulary
  applied to gas until that changes.
- ISO 9001's sixth edition lands 16 September 2026. Re-check clause 4.4 then.

## Sources

- ISO 9001:2015 cl. 4.4.1 and 4.4.2. ISO/TC 176/SC 2 announcement of FDIS approval,
  7 August 2026; sixth edition due 16 September 2026.
- OMG BPMN 2.0.2, formal/2013-12-09; ISO/IEC 19510:2013 (identical to BPMN 2.0.1,
  confirmed current 2022).
- OMG CMMN 1.1, formal/2016-12-01, clause 1 Scope and clause 2.4 BPMN Compatibility
  Conformance.
- OMG DMN 1.5, formal/24-01-01, clause 5, clause 11.1.2, Annex A.4.
- Flowable 8.0.0, released 2026-02-27; Flowable DMN documentation on JUEL; Flowable
  CMMN documentation on the Completion Neutral Rule.
- Camunda, *How CMMN never lived up to its potential*, 20 August 2020.
- Bule, M. & Polančič, G., *Systems* 14(2):180, 2026. Routis et al., *SoSyM* 20(6), 2021.
- Bruce Silver, *BPMN and Business Process Architecture*, methodandstyle.com,
  29 December 2016.
- APQC, *Understanding the Elements of APQC's Process Classification Framework*;
  PCF Utilities 8.0 (Excel, 20 August 2026); PCF Utilities Members' BPMN 6.1.0.
- IEC 61968-6:2015 ed. 1.0, clauses 1, 4.1, 4.2, 5.3-5.5, Annexes A and B.
  IEC 61968-11:2013 ed. 2.0. IEC 61968-4:2019 ed. 2.0. IEC 61968-9:2024 ed. 3.0.
  IEC 61970-301:2020 ed. 7.0.
- CIM `Work` package class definitions (published CIM100 renderings; the IEC text is
  paywalled and was not read directly).
- The Open Group, ArchiMate 3.2 Specification, October 2022, and the 3.2 reference cards.
- ASQ, SIPOC+CM. IATF 16949 FAQ, 7 March 2019 (searched: no occurrence of "turtle").
- Oracle Utilities Reference Models, WAM v2.1 (5.8 Manage Work and Projects).
- EPRI Utility Business Capability Model. TM Forum TR239. MultiSpeak V5.0 (NRECA).
- Observed practice: the process design documents of one combined gas and electric
  work and asset management programme, whose PDD structure informed the specification
  field set (see `../\_Collab/knowledge-pack/20\_PROVENANCE.md`, statement S8).

Not verified and deliberately not asserted: the ArchiMate specification's own appendix
on its relationship to BPMN (behind Open Group SSO); IEC 61968-6 Table 3's class list
(beyond the public preview); whether Flowable 8.0.0 executes DMN decision services
beyond decision tables; whether APQC PCF 8.0 still has thirteen level-1 categories.

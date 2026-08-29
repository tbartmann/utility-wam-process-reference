# Contractor management: why it left the work sequence

Research note, 2026-08-28. Written to settle one question: does any recognised process
framework place contractor or supplier management as a sequenced step inside a work
lifecycle, and if not, where does it belong?

Short answer: no framework consulted does, several explicitly do the opposite, and two
of them moved it out of the sequence in their most recent revisions. The reference has
been changed to match. What follows is the evidence, the counter-evidence, and the
design that came out of it.

---

## 1. What the reference used to say

Until this revision, category 5.0 Manage Contractors and Partners sat between 4.0
Dispatch and Execute Field Work and 6.0 Close Work, Settle Cost and Update Records,
inside a band captioned "Runs in sequence for a single piece of work." [repo]

The model was already arguing with itself about this. The lifecycle slide drew five
stages, not six, and merged contractors into delivery as "4.0 / 5.0 — Assigned,
dispatched and executed by internal or contract crew." [repo] A category that has to be
merged with its neighbour to draw the sequence is not a stage in that sequence.

The provenance record says the category was researched separately rather than observed
in either source programme — all five groups graded R/0 against statement S3, where the
lifecycle categories around it are P/2 from programme process flows. [repo] So the
placement was not lifted from an observed sequence. It was a judgement, and it was never
revisited: Round 1 endorsed the demand-to-close sequence in general terms, and Round 2
mapped the category to a standards clause, which validated its content and left its
position untested. [repo]

## 2. What the frameworks actually do

### ISO 55001:2024 — the lifecycle is enumerated, and contracting is not in it

Clause 8 has three subclauses and no fourth: 8.1 Operational planning and control
including life cycle management, 8.2 Control of change, 8.3 Externally provided
processes, products, technologies and services.
[source: ISO 55001:2024, second edition 2024-07, table of contents]

ISO/TC 251's own guidance says what 8.1 now carries: "This subclause now addresses
explicitly life cycle processes (creation, acquisition, utilization, maintenance,
improvement, renewal, and disposal of assets)."
[source: ISO/TC 251, ISO 55001:2024 Updated Guidance on Asset Management System
Requirements, 2024]

That is the load-bearing fact. The standard enumerates the lifecycle stages, and
external provision is not among them — it is a separate subclause sitting alongside.
The same guidance confirms 8.3 is the renamed 2014 clause: "The term outsourcing has
changed to externally provided processes, products, technologies and services in line
with the ISO Harmonized Structure. The requirements are not changed substantially."
[source: ISO/TC 251 guidance, 2024]

Read the clause itself and it is plainly a control, not a stage. It requires the
organisation to determine what is externally provided "including the scope and
boundaries of these, as well as their interfaces with the organization's own processes",
to assign responsibility, to share knowledge, and to ensure the externally provided work
"meet[s] the relevant requirements of Clauses 7 and 8" and is "monitored in accordance
with 9.1." [source: ISO 55001:2024 clause 8.3, reproduced in NEN, Guide for Outsourcing
Asset Management Activities v1.0, July 2025, Annex A, hosted on the ISO/TC 251
committee site] A stage has a start condition, an end condition and a handoff. This has
none of the three; it has a trigger — the fact of external provision — and a set of
controls that reach back across two whole clauses.

The same TC 251 guide states the point directly: outsourcing concerns "activities that
may take place during various phases of the asset lifecycle." [source: NEN guide, §5]

ISO 55002:2018 §8.3 adds the exit obligation — "a process of handing over and/or taking
back control over asset(s) and/or the asset management activity" — and its Annex B
contemplates an owner who "outsources most or all of the asset management activities."
[source: ISO 55002:2018] A lifecycle stage cannot expand to cover the whole lifecycle.
A control can.

### ISO 9001:2015 — one clause, three different positions in the value chain

Clause 8.4 Control of externally provided processes, products and services applies when
"products and services from external providers are intended for incorporation into the
organization's own products and services", when they are "provided directly to the
customer(s) by external providers on behalf of the organization", and when "a process,
or part of a process, is provided by an external provider as a result of a decision by
the organization." [source: ISO 9001:2015 §8.4.1]

Three triggers at three different points in the value chain, handled by one clause. That
is only coherent if 8.4 is a control rather than a position. Annex A.8 says so: "All
forms of externally provided processes, products and services are addressed in 8.4."
[source: ISO 9001:2015 Annex A.8] And the operational clause does not contain a supplier
step — it points at the control: "The organization shall ensure that outsourced processes
are controlled (see 8.4)." [source: ISO 9001:2015 §8.1, final sentence]

Note: the ISO 9001 body text above is from a third-party full-text reproduction, not
ISO's own preview. The clause titles and structure are independently confirmed; treat the
wording as high confidence rather than certified. [judgment]

### GFMAM Landscape v3.0 — the document distinguishes a stage from a life-cycle-wide subject

Supply Chain Management is subject 6.8, in group 6 Delivery. Its context statement:
"Supply chain management includes all the activities necessary to acquire, manage,
maintain, and enforce contract and supplier management over the entire life cycle of an
asset, taking total cost of ownership into consideration. It includes purchasing,
inventory, warehousing, and contracting (authoring, negotiations, adoption, definition of
requirements, appraisal and selection of contractors, outsourcing-insourcing strategies,
and claim management)." [source: GFMAM Asset Management Landscape, Third Edition v3.0,
June 2024, p.81]

Two subjects earlier, the same document describes 6.2 Asset Creation & Acquisition as
"the stage in an asset life cycle where the organization decides on the specifications
and required outputs of an asset". [source: GFMAM v3.0, p.72]

The document uses stage language for one subject in the group and "over the entire life
cycle" for the other. That contrast is the clearest single piece of evidence available.
3.7 Resourcing Strategy and Management repeats the "over the entire life cycle" framing
for contracting and contractor selection. [source: GFMAM v3.0, p.41]

Two honest caveats. The Landscape contains no sentence saying its subjects are
non-sequential; do not claim one. [judgment] And GFMAM itself lists group 6 out of
numeric order in its own appendices — 6.2, 6.1, 6.5, 6.3, 6.4, 6.6, 6.7, 6.8 — which is
behaviour, not doctrine, but it is telling. [source: GFMAM v3.0, appendices 1 and 2]

Worth knowing for continuity: in the Second Edition (2014) supply chain sat in group 5
Organisation and People as S26 Procurement & Supply Chain Management. It has never been
in a lifecycle sequence in either edition. [source: GFMAM v3.0, Appendix 1]

### APQC — the framework this reference borrows its numbering from says numbering is not order

The reference has always described itself as APQC-style in its numbering and naming.
[repo] APQC is explicit about what that numbering does and does not mean:

"Although process elements are numbered ascendingly, it is important to understand this
does not imply that process elements occur in a certain order."
[source: APQC, Understanding the Elements of APQC's Process Classification Framework]

"The PCF is a catalog, or index, of an organization's process activities; it is an index
of what an organization does. It is important to note it is not how an organization
manages and executes its processes." [source: APQC PCF FAQs]

"APQC's PCF is designed to provide a list of work that is done in the organization; not
how the work is performed... Organizations should not adapt the PCF to mirror their
organization's structure, but instead should use the PCF as a 'pick list' of work that
could be done in their organization and align the order in which it happens (displayed in
process maps) to their organization's way of working." [source: APQC PCF FAQs]

Where APQC puts procurement: 4.2 Procure materials and services, under 4.0 Manage Supply
Chain for Physical Products, decomposing into 4.2.1 Provide sourcing governance and
perform category management, 4.2.2 Select suppliers and develop/maintain contracts, 4.2.3
Order materials and services, 4.2.4 Manage suppliers. [source: APQC PCF Cross-Industry
v7.4, August 2024] Supplier management is a sibling of ordering, not a stage after it.

More useful still: APQC has its own execute-then-close sequences, and none of them
contains a contractor stage. 13.2.3 Manage projects runs establish scope, identify
methodologies, develop plans, execute projects, review and report performance, close
projects. 5.3 Deliver service to customer runs initiate, execute, complete. 10.2 covers
asset construction with monitor work performance and undertake construction quality
control. No supplier step appears in any of them. [source: APQC PCF Cross-Industry v7.4]

A Utilities PCF exists — v7.2.1-en-UTIL, April 2020, APQC and IBM, 14 categories with an
industry-specific 14.0 Operate Utility Assets. Procurement sits at 4.2 exactly as in the
cross-industry framework. A full-text search of it returns zero hits for "contractor".
[source: APQC PCF Utilities v7.2.1]

One detail worth stealing, and this reference now has: APQC keeps element id 10280
"Manage suppliers" stable while its dotted number differs between the cross-industry
(4.2.4) and utilities (4.2.5) frameworks. Identity and position are separate things.
[source: APQC PCF v7.4 and Utilities v7.2.1]

### TM Forum eTOM — the architectural precedent for keeping the category whole

eTOM models Supplier/Partner Relationship Management as process 1.1.4, one of four
horizontal groupings in the Operations area, and describes it as: "This horizontal
functional process grouping supports the core operational processes, both the customer
instance processes of Fulfillment, Assurance and Billing and the functional operations
processes." [source: TM Forum GB921 Addendum D, Business Process Framework (eTOM)
v12.2, April 2012, p.180]

The decomposition proves the span. Its six level-2 processes each serve a different
operational vertical: S/PRM Support & Readiness serves Operations Support & Readiness,
S/P Requisition Management serves Fulfillment, S/P Problem Reporting & Management and
S/P Performance Management serve Assurance, S/P Settlements & Payments Management serves
Billing, and S/P Interface Management crosses all of them. [source: GB921 Add. D v12.2]

This is the design this reference now copies: one coherent category, marked as spanning,
with each of its groups mapped to the lifecycle stage it attaches to. eTOM goes further
and carries supplier/partner management twice — also as 1.2.4 Supply Chain Development &
Management in the strategic area — and never once as a stage. [source: GB921 Add. D v12.2]

Caveat: verified against the 2012 v12.2 release. Whether the current Open Digital
Framework preserves this wording is unconfirmed; cite the release. [judgment]

### ASCM SCOR v14 — the expected counter-example, which moved the other way

SCOR has Source as a level-1 process, so at first look it supports a sourcing stage. Two
things spoil that reading.

First, SCOR is a supply-chain model, not a work-execution model, and says so: it "does
not attempt to describe every business process or activity. Specifically, SCOR does not
address sales and marketing, including demand generation; product development; or
research and development." [source: ASCM SCOR Digital Standard v14.0, 2025] Its sequence
is a materials flow, not a work order.

Second, ASCM moved contracting out of Source. In SCOR-DS, Contracts and Agreements is
OE6 under Orchestrate — a level-0 process explicitly added to "multi-directionally link
supply chain strategy to Plan and the rest of the processes", drawn as a double infinity
diagram because the model is "no longer linear". OE6 decomposes into create contract and
SLA, receive and update, record and distribute, activate or archive, review contract
performance, identify performance issues and opportunities, identify resolution and
improvements. [source: ASCM SCOR DS Quick Reference Guide]

So the one framework expected to argue for a sourcing stage draws exactly the
distinction this revision draws: transacting with a supplier sits in the flow, managing
the supplier and its contracts sits across it.

### ISO 44001 — the honest counter-evidence

ISO 44001:2017 Collaborative business relationship management systems is a genuine
partial counter-example. Its clause 8 really is an eight-stage sequence: operational
awareness, knowledge, internal assessment, partner selection, working together, value
creation, staying together, exit strategy activation. [source: ISO 44001:2017, edition 1,
2017-03, stages per the BSI published abstract]

So "nobody sequences supplier management" is false, and should not be claimed. The
correct reading is narrower and stronger: the sequence ISO 44001 defines is the lifecycle
of the relationship, not of the work. A single relationship persists across many jobs —
ISO's own abstract contemplates application to "multiple partner alliances, consortia,
joint ventures, networks, extended enterprise arrangements and end-to-end supply chains"
or "full application organization-wide". [source: ISO catalogue entry, ISO 44001:2017]
ISO 44001 exists because relationship management needed a lifecycle of its own, separate
from the delivery lifecycle it overlays. [judgment]

I could not confirm that the eight stages carry subclause numbers 8.1 to 8.8; cite them
as the stages of clause 8. No primary ISO statement was found saying the relationship
lifecycle runs in parallel to a delivery lifecycle — say "separate from", which is
supported, not "parallel to", which is not. [judgment]

### Regulatory — the obligations attach to the task, not to a phase

49 CFR 192 Subpart N, Qualification of Pipeline Personnel, never uses the words
contractor or employee. It regulates "individuals performing covered tasks", where a
covered task is "an activity, identified by the operator, that... is performed on a
pipeline facility... is an operations or maintenance task... is performed as a
requirement of this part; and... affects the operation or integrity of the pipeline."
[source: 49 CFR 192.801, 192.805] Records must be kept "while the individual is
performing the covered task." [source: 49 CFR 192.807(b)]

The regulation is a matrix of covered tasks by qualified individuals. Employment
relationship is not an axis in it. PHMSA confirms the reach: "Each operator is
responsible for ensuring that its contractors and vendors comply with the requirements
of the operator's qualification program." [source: PHMSA, Pipeline Safety: Operator
Qualification Frequently Asked Questions, 86 FR 3956, 15 January 2021 — note PHMSA
states the FAQs are not rules and create no new obligations]

OSHA process safety management makes the same shape visible. 1910.119(h) Contractors is
one of fourteen standing elements, (c) through (o), next to mechanical integrity and
management of change. It applies to "contractors performing maintenance or repair,
turnaround, major renovation, or specialty work" — four unrelated activity types spanning
routine O&M, planned outage and capital modification — and excludes work by risk, not by
phase: "incidental services which do not influence process safety". Its employer duties
run as a loop: evaluate at selection, inform, control entry and exit, "periodically
evaluate the performance of contract employers", maintain an injury log.
[source: 29 CFR 1910.119(h)] Note that the one element in that list which is phase-bound,
(i) Pre-startup safety review, is named as such. Contractors is not.

On the electric side, NERC CIP-013-2 requires a supply chain cyber security risk
management plan covering procurement planning, procurement itself, vendor incident
coordination and remote access during operations, and "transitions from one vendor(s) to
another vendor(s)". [source: NERC CIP-013-2 R1] One plan, four phases.

## 3. What was changed, and why that design

Contractor management stays one category. Splitting it across 2.0, 3.0, 4.0 and 5.0 would
be defensible on a purist reading of ISO 55001, but it would destroy the ability to
scope, evaluate or buy contractor management as a capability — which is exactly what it
is used for in vendor evaluation. eTOM shows the alternative: keep the grouping whole,
mark it horizontal, and record which vertical each member serves. [judgment]

So: Manage Contractors and Partners moved from 5.0 to 16.0, into Foundations and
Enabling, whose caption already read "Support every lifecycle stage rather than sitting
inside the sequence" — the right description, applied to the wrong set of categories.
[repo] Close Work moved 6.0 to 5.0 so the lifecycle reads 1 to 5 with no gap and no lie.
The specialised block became contiguous at 6.0 to 11.0, which also ended the anomaly of
Joint Use sitting at 16.0 outside its own band.

Each 16.x group now records the lifecycle and enabling groups it attaches to, in
model.json:

| Group | Attaches to |
|---|---|
| 16.1 Qualify and onboard contractors | 14.2 skills and certification, 13.4 procure goods and services, 8.1 compliance |
| 16.2 Award and assign contracted work | 2.3 estimate, 2.4 authorise, 3.1 forecast capacity, 3.5 crews and resources |
| 16.3 Oversee contractor execution | 4.1 assign and dispatch, 4.2 execute, 4.3 capture evidence, 4.4 field safety |
| 16.4 Settle and evaluate | 5.1 verify and close, 5.2 capture and settle cost, 15.2 measure and improve |
| 16.5 Integrate with contractor systems | 15.5 integrate systems, 13.7 integrate with suppliers |

These are attachment points, not an order. 16.1 runs before any specific work exists,
16.3 runs concurrently with 4.0, and 16.4 straddles 5.0. [judgment]

Every category, group and process also gained a permanent uid, and the pre-revision
number is kept as legacy_id with a full crosswalk at build/eam/id_crosswalk.csv. The
dotted number is now an index; the uid is the identity. This is APQC's own practice and
it is what makes a future restructure cheap instead of dangerous. [source: APQC PCF v7.4
and Utilities v7.2.1] [judgment]

The Round 2 standards mapping did not need changing on its merits — ISO 55001:2024 8.3
primary, GFMAM 6.8 Supply Chain Management primary. Those mappings were always right.
They were mapping a category that was in the wrong place. [judgment]

## 4. What this does not claim

The reference still asserts no conformity with ISO 55001 and no coverage of the GFMAM
Landscape, and is not an APQC-licensed framework. The numbering convention is
APQC-style; the content is not APQC's. Category boundaries remain a convention, and the
empirical base is still two utility programmes. This revision changed placement,
numbering and identifiers. It changed no process, no name and no commodity tag.

## 5. Sources

- ISO 55001:2024, Asset management — Asset management system — Requirements, second
  edition 2024-07. Clause structure verified from the ISO preview.
- ISO/TC 251, ISO 55001:2024 — Updated Guidance on Asset Management System Requirements,
  2024. https://committee.iso.org/files/live/sites/tc251/files/guidance/ISO%20TC251%20ISO55001%20Rev3.pdf
- NEN / Dutch Asset Management Standards Committee, Guide for Outsourcing Asset
  Management Activities, v1.0, July 2025, Annex A (reproduces ISO 55001:2024 §8.3 and
  ISO 55002:2018 §8.3). Hosted on the ISO/TC 251 committee site.
- ISO 55001:2014, first edition 2014-01-15 (clause 8.3 "Outsourcing", for the rename).
- ISO 55002:2018, second edition 2018-11.
- ISO 9001:2015, fifth edition 2015-09-15, §8.1, §8.4, Annex A.8.
- ISO 44001:2017, Collaborative business relationship management systems — Requirements
  and framework, edition 1, 2017-03; Amd 1:2024. Stage names per the BSI abstract.
- GFMAM, The Asset Management Landscape, Third Edition v3.0, June 2024.
  https://gfmam.org/sites/default/files/2024-06/GFMAM_AM_Landscape_v3.0_English_2024.pdf
- APQC, Process Classification Framework Cross-Industry v7.4, August 2024.
- APQC, Process Classification Framework Utilities v7.2.1-en-UTIL, April 2020 (APQC and IBM).
- APQC, Understanding the Elements of APQC's Process Classification Framework, and PCF FAQs.
- TM Forum, GB921 Addendum D, Business Process Framework (eTOM) v12.2, April 2012.
- ASCM, SCOR Digital Standard v14.0, 2025, and the SCOR DS Quick Reference Guide.
- 49 CFR Part 192 Subpart N (§§192.801, 192.805, 192.807), current eCFR text.
- PHMSA, Pipeline Safety: Operator Qualification Frequently Asked Questions, 86 FR 3956,
  15 January 2021.
- 29 CFR 1910.119(h), Process safety management of highly hazardous chemicals — Contractors.
- NERC Reliability Standard CIP-013-2, Cyber Security — Supply Chain Risk Management, R1.

Not consulted or not obtainable: APQC PCF v8.0 (published August 2026, gated); the
current TM Forum Open Digital Framework release; EPRI, EEI, CIGRE and IEEE material on
contractor management, all member-gated or paywalled. ISO 45001:2018 §8.1.4 Procurement
sits inside 8.1 Operational planning and control and is a further supporting citation if
one is wanted; its sub-subclause breakdown was not verified.

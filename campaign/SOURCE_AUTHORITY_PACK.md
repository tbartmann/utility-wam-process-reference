# Source Authority Pack

**Binding on all three platforms for the process specification campaign.** Compiled
2026-08-28 from primary and issuing-body sources. This is the only source list. If a
source is not in here, it does not go in the reference — raise it as a gap instead.

Why it exists: three platforms specifying fifteen categories independently will produce
fifteen incompatible specifications unless they draw on the same authorities. The
consensus method depends on the platforms disagreeing about *findings*, not about
*inputs*.

---

## 0. How to cite

### The status ceiling — added 2026-08-29, and it is enforced

A citation status is a claim about what somebody actually read. Until 2026-08-29 nothing
checked whether the claim was earned, and all three specification files carried `verified`
against standards this project does not hold — **24 in category 1.0, 18 in 2.0, 32 in the
3.0 submission.** Claude wrote the first ones and the pack, asserting `verified` for
ISO 55001, ISO 9001 and IEC 61968, taught the other platforms to do the same.

`build/eam/vocabulary.json` now carries `source_status_ceiling`, and no source may be cited
above its ceiling:

| Group | Ceiling | What is in it |
|---|---|---|
| **Held in full** | `verified` | EN 17007, APQC PCF, the GFMAM Landscape — obtained, or free and read |
| **Public law** | `regulation` | CFR, U.S.C., MUTCD, USACE nationwide permits, state codes |
| **Member-gated** | `consensus` | SMRP, AACE, CGA, EPRI, API RP, IAM, GPTC, MultiSpeak |
| **Paywalled** | `clause-verified` | Every ISO, IEC, EN, ASTM, ANSI, IEEE, ASME, ASCE standard |

Anything unlisted defaults to `clause-verified`. **`clause-verified` forbids paraphrasing
content you have not read** — cite the clause number and title, and say what you are
inferring rather than presenting it as the standard's words.

`build/eam/sources.py` implements the lookup once. The generators clamp as they write, so
an over-claim cannot be authored; `validate_spec.py` rejects, so one cannot be merged.
**A ceiling is raised only by obtaining the text** — put the document in `Tim Evidence/`,
register it with its sha256, and change the entry in the same commit. Never by argument.


Every field in a specification carries a `sources` entry with a status. Never upgrade a
status, and never reproduce a paywalled clause's content from a paraphrase found online.

| Status | Meaning |
|---|---|
| `verified` | Read verbatim from official or issuing-body text. |
| `regulation` | Verbatim from current eCFR or equivalent primary regulatory text. |
| `clause-verified` | Clause number and title confirmed from official contents; body paywalled and NOT read. Cite by reference; do not paraphrase the content. |
| `consensus` | Published guidance from a recognised industry body. Not a standard, not law. |
| `judgment` | Professional inference. Attributed to nobody. |

Two standing prohibitions. **Do not turn a `clause-verified` citation into content** — every
"EN 13306 maintenance types" tree circulating online is an uncited paraphrase, and none
of them may be used. **Do not cite a vendor glossary, a conference report or sponsored
analyst research as a definitional source.**

---

## A. Cross-commodity foundation — applies to every category

### A1. Maintenance process — the spine

| Source | Edition | What it gives you | Status |
|---|---|---|---|
| **EN 17007** *Maintenance process and associated indicators* | 2017-10, CEN/TC 319 | **The process reference model.** Cl. 5.2 is the process profile the specification field set is built from. Cl. 5.1 gives three process families. Table 2 records its own notation as BPMN 2.0. Sixteen level-1 processes and **101 level-2 processes**, all now in `vocabulary.json` — do not cite a level-1 code where a level-2 one fits. Clause map: 6.2 MAN, 6.3 PRV, 6.4 COR, 6.5 ACT, 6.6 IMP, 6.7 HSE, 6.8 BUD, **6.9 DOC**, **6.10 DTA**, 6.11 IST, 6.12 MRQ, 6.13 OPT, 6.14 RES, 6.15 SER, 6.16 SPP, 6.17 TOL. | Cl. 1, 5.1, 5.2, contents and the clause-6 process names `verified` from the supplied text |
| **EN 13306** *Maintenance terminology* | 2017-11 | Cl. 2 fundamental terms (`verified`). Cl. 7 maintenance types — preventive predetermined/condition-based, corrective immediate/deferred. **Annex E criticality matrix.** | Cl. 2 `verified`; cl. 7, Annex E `clause-verified` |
| **EN 13460** *Documentation for maintenance* | 2009 | Cl. 3.8 work order definition (`verified`). **Annex B "Work order information items"** — the only standards-body work-order field list found anywhere. Normatively references EN 13306:2001, two editions stale. | Cl. 3.8 `verified`; Annex B `clause-verified` |
| **EN 15341** *Maintenance KPIs* | **2019+A1:2022** | Eight indicator groups: PHAi HSEi Mi Pi Ei O&Si A&Si ICTi. **O&S9–O&S22 Planning and Control**; O&S23–O&S28 Productivity Effectiveness; HSE1–HSE22. Cl. 5.4 defers to EN 17007 for process definition. | Matrix `verified`; indicator names `clause-verified` |
| **EN 16646 / EN 17485 / EN 17666 / EN 17948** | 2014 / 2021 / 2022 / **2024-11** | Maintenance within physical asset management; asset value framework (its "Triggers" language at cl. 5.3, 5.6 is a second vocabulary for demand origination); maintenance engineering; **maintenance management and functions**. | `clause-verified` |
| **EN 13269** *Guideline on preparation of maintenance contracts* | 2016 | Cite for **contracting only** — category 16.0. Says nothing about operations. | `clause-verified` |
| **ISO 14224** *Collection and exchange of reliability and maintenance data* | 2016, Ed. 3 | Cl. 9.5 failure data, **cl. 9.6 maintenance data** (9.6.2 maintenance categories, 9.6.3 reporting), Annex B normative parameter notation, Annex E KPIs. | Contents `verified`; clause bodies `clause-verified` |
| **SMRP Best Practices** | **7th Edition** | Pillar 5 Work Management metrics. Verified numbers: 5.3.1 Planned Work, 5.3.2 Unplanned, 5.4.1 Reactive, 5.4.2 Proactive, 5.4.3/5.4.4 Schedule Compliance, 5.4.6 Aging, 5.4.7 Cycle Time, 5.4.8/5.4.9 Backlog, 5.4.11 Overdue, 5.4.12 Yield, 5.4.14 PM Compliance, 5.5.x resourcing ratios, 5.6.1 Wrench Time, 4.1 Rework, 5.7.1 CI Hours, 3.1 Criticality Coverage. **Numbering changed between editions — cite the edition.** SMRP and EFNMS publish a harmonised metric list. | `consensus`; definitions read from a 2018-era deck are `verified` for those metrics only |

**Withdrawn, do not cite as current:** IEC 60300-3-14:2004 (withdrawn 2024-08-09; the 2024
Ed. 2 is retitled *Supportability and support* and is no longer a maintenance-process
document). EN 15221-3 and -5 (withdrawn; -5 superseded by EN 15221-8:2025).

### A2. Asset management system

| Source | Edition | Use it for | Status |
|---|---|---|---|
| **ISO 55001** — cite as **ANSI/ASTM/ISO 55001-2024** for a US audience | **2024-07, Ed. 2** | Cl. 8.1 operational planning and control **including life cycle management** — the lifecycle is enumerated here; cl. 6.2.2 asset management planning; cl. 6.3 planning of changes; cl. 8.2 control of change; cl. 8.3 externally provided processes. There is no cl. 8.4. Genuinely commodity-neutral. **ASTM International adopted it as an American National Standard**, so for US utilities the ANSI/ASTM designation is the stronger citation. | `clause-verified` |
| **ISO 55000 / 55002** | 2024 / 2018 | Vocabulary; application guidance. ISO 55002 cl. 8.1.2 decision-making criteria, 8.1.3 operational planning processes. ISO/CD 55002 revision in progress. | `clause-verified` |
| **GFMAM Asset Management Landscape** | **3rd ed. v3.0, 2024-06**, ISBN 978-1-7774676-8-5 | **7 subject groups, 40 subjects — the definition of the discipline, and free.** Group 6 Delivery is the asset lifecycle: 6.2 Asset Creation & Acquisition, 6.4 Asset Operation, 6.5 Maintenance Delivery, 6.6 Incident Management and Response, 6.7 Asset Repurposing or Disposal, 6.8 Supply Chain Management. Group 3 carries 3.2 Demand Analysis, 3.4 Planning, 3.6 Life cycle Value Realization, **3.8 Shutdown and Outage Strategy and Planning**. Crosswalked in `build/eam/gfmam_crosswalk.json`. | `verified` |
| **IAM Asset Management — An Anatomy** | **v4, 2024-07-01** | Corroboration only. v4 moved to a **10-box capability model** and **defers to the GFMAM Landscape 3rd ed. for the subjects** — so cite GFMAM for subjects, not the Anatomy. There is **no North America–specific edition**, and the widely repeated "39 subjects" figure is the Landscape's **second** edition. | `consensus` |
| **IAM SSG 15 & 17** *Maintenance Delivery and Asset Operations* | v1.0, 2019-04 | Industry-body corroboration only. Member PDF. | `consensus` |
| **EPRI** | programme-based, no single framework | Member-gated. There is no public EPRI process reference comparable to EN 17007 or the GFMAM Landscape; the retrievable material is programme analytics (Program 34 Transmission Asset Management Analytics, the Distribution portfolio) and older reports such as *Power Delivery Asset Management Decision Making Process* (1016834, 2008), whose generic framework is set goals → assess performance → identify gaps → develop options → evaluate and optimise → implement → monitor. **Useful for method, not for process structure. Do not cite EPRI for a process the model needs to name.** | `consensus`, member-gated |
| **ISO 9001** | 2015 (**6th edition due 2026-09-16**) | Cl. 4.4.1 a)–h) as the management-system corroboration of the EN 17007 field set. Cite the clause, not the year; re-check on publication. | `clause-verified` |

### A3. Process framework structure — convention only, no asset management authority

**APQC PCF** — **in the repository since 2026-08-29, so stop citing it from memory.**
Cross-Industry **v8.0** (Excel, generated 2026-02-25) and **Utilities v7.2.1** (Excel, with
a difference index against v6.1.0) plus **Utilities v7.2.2** (PDF, March 2025). There is
**no Utilities v8.0** — the cross-industry framework has moved on and the industry version
has not.

Extracted to `build/eam/apqc_pcf_utilities.json` (2,073 elements, 14 categories) by
`build/extract_apqc.py`. **Read the JSON; do not guess element numbers.** The `pcf_id` is
APQC's permanent identifier and survives renumbering — the same practice this repository
follows with `uid`.

Used for numbering, verb-noun naming and **structural precedent** only. APQC's own
statement, quotable: *"Although process elements are numbered ascendingly, it is important
to understand this does not imply that process elements occur in a certain order."*
Levels: 1 Category, 2 Process Group, 3 Process, **4 Activity**, 5 Task. **Flow modelling
begins at Level 4, never above.** A Members' BPMN version exists but is pinned at 6.1.0.

Two things to know before using it:

- **Only categories 10.0 *Acquire, Construct, and Manage Assets* and 14.0 *Operate Utility
  Assets* carry utility content.** The other twelve are the cross-industry framework.
- **The v7.2.2 PDF carries a publication error.** Its 10.4 group header repeats "Maintain
  productive assets (19238)" while listing the five disposal processes beneath it; PCF ID
  10940 "Dispose of assets" appears nowhere in that PDF. The v7.2.1 Excel is right. Do not
  correct anything against that header.
- **The licence is conditional and the condition is attribution.** The Utilities PCF is
  jointly APQC and IBM. They grant a perpetual, royalty-free licence to use, copy, publish,
  modify and create derivative works, *provided* copies carry the copyright notice and
  derivative works carry APQC's attribution paragraph. Both are in `_copyright` and
  `_attribution` in the extracted JSON. **If your deck or workbook shows an APQC element
  number or name, it must carry the attribution.** Contrast `Tim Evidence/`, which is
  gitignored because EN 17007 and ISO 55001 may not be redistributed at all.

**Not to be used as content sources**, but useful as structural precedent when a category
needs one: TM Forum eTOM GB921 (S/PRM as a horizontal), ASCM SCOR v14 (Orchestrate as a
cross-cutting layer).

---

### A2-bis. EN 17007 read properly — corrections and limits, added Round 1, 2026-08-29

The full standard is in `Tim Evidence/`. Read it rather than working from the summary.
Four things it settles:

1. **The clause numbers in the row above are corrected.** MAN was recorded at 6.9 and is
   **6.2**; DOC was recorded at 6.10 and is **6.9** — 6.10 is DTA. Both wrong numbers had
   reached shipped citations, because `validate_spec.py` checked clause numbers only for
   level-2 processes. It now checks both levels. Re-check any citation you have already
   drafted.
2. **There are 101 level-2 processes, not 11.** Only PRV, COR and ACT are numbered to
   level 3 in the contents; the rest sit inside their level-1 clause and have no clause
   number of their own, but they have names and those names are usually a far better
   citation than the level-1 code. `BUD.2 Create a budget estimate for regular
   maintenance` and `BUD.3 … for infrequent or exceptional maintenance tasks` say more
   than `BUD`. `DOC.6 Manage the way in which operational documentation is made
   available` says more than `DOC`. TOL.1 is not machine-readable in the supplied text and
   is recorded as absent rather than guessed.
3. **EN 17007 has no funding, approval or authorisation process.** The only occurrences of
   "approval" and "authorized" in clause 6 are SER.4 acceptance of an external service and
   DOC.5 document update rights. `MAN.4 Prepare and negotiate the budgets` is the closest
   and it is budget setting, not work authorisation. If your category contains an approval
   gate, say that EN 17007 does not cover it rather than stretching MAN over it.
4. **MRQ is an input to someone else's design, not a design process.** MRQ.4 reads
   "Oversee or **contribute to** the drafting of specifications" and MRQ.6 "**Participate
   in** the analysis and choice of options". EN 17007 assumes the item already exists and
   maintenance feeds requirements into its design. Utility construction design — a new
   line extension, a main replacement — is asset creation and is outside EN 17007
   entirely. ISO 55001:2024 cl. 8.1 and ISO 9001:2015 cl. 8.3 cover it; EN 17007 does not.

### A3-bis. What the APQC crosswalk found — read this before judging your own category

`build/make_apqc_crosswalk.py` maps all 38 level-3 processes in APQC categories 10.0 and
14.0 against this model, **by hand** — a coverage claim a machine guessed by string
similarity is worth nothing. Twelve are out of scope (corporate real estate, generation,
water treatment, real-time network optimisation). Of the twenty-six in scope: **12 covered,
6 partial, 8 absent.** Full reasoning in
`research/APQC PCF Utilities - Read Against the Model.md`.

The eight absences, because they affect more categories than 2.0:

| APQC | Process | Why it matters to your category |
|---|---|---|
| **14.1.6** | Perform planned network operation (19285) | Submit, approve, schedule and execute switching for **planned** work, and co-ordinate with maintenance and construction. The model consumes a clearance (2.6.3, 4.4.4) and switches only during restoration (9.3.2). If your category assumes a clearance arrives from somewhere, say so explicitly and cite 29 CFR 1910.269(m) rather than inventing an owner |
| **10.2.2** | Perform utility network planning (19213) | Network demand forecasting, capacity assessment, network modelling, protection design. 3.1 forecasts WORK demand, not network demand. This is where most capital work originates |
| **10.2.1** | Manage capital program (19209) | Capital investment plan, programme monitoring, construction financing. 2.4.1 validates funding for one work item; nothing produces the budget it checks against. ISO 55001:2024 cl. 6.2.2 expects this layer |
| **10.2.6** | Commission new assets (11280) | Schedule commissioning, **co-ordinate energization with network operations**, capture commissioning records. 6.3 commissions a metering endpoint and nothing else |
| **10.4.5** | Waste and hazardous goods management (16970) | Spoil, contaminated soil, PCBs, transformer oil, asbestos pipe wrap. 7.4.4 disposes of vegetation debris and that is all |
| **10.4.2** | Decommission productive assets (19258) | The model retires the record (12.1.6) and the accounting (5.3), never the plant |
| **14.1.4** | Monitor network status (19278) | Switch and valve state, historical state, alarms. Possibly a SCADA boundary — but absent by omission, not by decision |
| **14.1.2** | Develop network operational plans (11266) | Contains 19270 create switching and reconfiguration plans — the planning half of 14.1.6 |

One misplacement: **10.4.4 Perform abandonment** maps to `8.6.6 Purge, seal and abandon
facilities`, inside *8.6 Manage gas pressure and odorization*. Abandonment is a lifecycle
end state governed by 49 CFR 192.727 in its own right, not a pressure task.

**Where APQC is coarser, the model wins.** APQC compresses into `10.3.1 Plan asset
maintenance` what this model spreads across six groups. APQC is a benchmarking taxonomy,
not a process model. Use it as evidence of an **omission** when it has a process the model
lacks entirely; never use it to flatten a distinction the model makes deliberately.

**What to do with this in your round.** Do not add groups or renumber anything — the
taxonomy question is open and belongs to the user. If your category touches one of the
eight, record it in your spec file's `gaps` array in the same words, and cite the APQC
`pcf_id`. That is how three platforms produce one finding instead of three.


### A4. The asset lifecycle gap — six themes both frameworks say are missing

`build/eam/gfmam_crosswalk.json` tests the model against the **GFMAM Asset Management
Landscape 3rd ed.** — 40 subjects, and unlike APQC this one *is* an asset management
authority. Result: 12 covered, 13 partial, **6 absent**, 9 out of scope.

Crossing that against the APQC result gives **six themes absent in both**, authored
independently from different documents on different axes. That clears this repository's
promotion threshold of two independent organisations, and ISO 55001:2024 cl. 8.1 — which
requires life cycle management explicitly — is the standards leg.

| Theme | APQC | GFMAM | Standards basis |
|---|---|---|---|
| Planned outage, shutdown and switching | 14.1.6, 14.1.2 | **3.8 Shutdown and Outage Strategy and Planning** | 29 CFR 1910.269(m), (d) |
| Asset operation | 14.1.4, 14.1.2 | **6.4 Asset Operation** | — |
| Asset creation, commissioning, energisation | 10.2.6, 10.1 | **6.2 Asset Creation & Acquisition** | ISO 55001 cl. 8.1 |
| Asset demand analysis and network planning | 10.2.2 | **3.2 Demand Analysis**, 3.4 | ISO 55001 cl. 6.2.2 |
| Capital programme and whole-life value | 10.2.1 | 3.4, **3.6 Life cycle Value Realization** | ISO 55001 cl. 8.1 |
| Decommissioning, disposal, waste | 10.4.2, 10.4.5 | **6.7**, 3.3 | 49 CFR 192.727 |

GFMAM defines subject 3.8, verbatim, as *"An organisation's processes for the
identification, planning, scheduling, execution, and control of work related to shutdowns,
turnarounds, or outages (STOs)."* The model performs none of those five verbs for a
**planned** outage — it consumes the clearance at 2.6.3 and 4.4.4 and switches only during
restoration at 9.3.2.

**CLOSED 2026-08-29 — the model now has an Asset Lifecycle band.** The user's decision
was to include the asset lifecycle, appended so that nothing renumbers. Categories 1.0 to
16.0 keep their ids, uids and legacy_ids; the campaign is unaffected.

| New | Name | Closes |
|---|---|---|
| **17.0** | Plan the Network and Capital Programme | network demand and capacity, solutions, gas class location, capital programme, whole-life value |
| **18.0** | Operate the Network for Planned Work | switching plans, outage approval, notification, switching execution, **clearance issue**, return to service |
| **19.0** | Commission, Decommission and Dispose of Assets | commissioning and energisation, decommissioning, waste and hazardous materials, disposal and transfer |

**18.0 is work-facing only, by decision.** It covers the network operations that gate work
already in this model. Real-time monitoring, alarm handling, optimisation and protection
settings are SCADA, ADMS and DERMS functions and are **out of scope by decision, recorded
as such** — see APQC 14.1.4 in the crosswalk, which is now `scope` rather than `absent`.

Both crosswalks now show **zero absences**. What remains is `partial` with the remainder
named, or `scope` with the reason.

**What this means for your round.** The model is organised on a **work** axis — identify,
plan, schedule, execute, close. The new band is on the **asset** axis — plan, create,
operate, dispose. The work axis is what happens *inside* maintain. Every category now
carries a `lifecycle` field saying which stage it serves, so you can see where yours sits.

Two practical consequences:

1. **A clearance is not a permit.** A permit is issued by an external authority — the
   one-call centre, a municipality, a railroad. A **clearance** or permit-to-work is issued
   by network operations at **18.4.4** against a switching plan approved at 18.2.2, under
   29 CFR 1910.269(m). If your category consumes one, cite 18.4.4 as its producing process
   rather than treating it as an input that arrives from nowhere. This affects 3.0 and 4.0
   directly.
2. **Still do not add categories, groups or processes.** 17.0 to 19.0 were added by the
   user's decision after two frameworks independently found the same six absences. If your
   category turns up something else, that is a finding for `gaps`, not a change for you to
   make.

**Also: EN 17007 is not ISO/IEC 17007.** EN 17007:2017 *Maintenance — Maintenance process
and associated indicators* is CEN/TC 319. ISO/IEC 17007 is *Conformity assessment —
Guidance for drafting normative documents*. Different committees, different subjects,
similar numbers. The supplied copy is misnamed `iso-170072017.docx` by whoever posted it.
If anyone tells you the process spine is a conformity-assessment standard, this is why.

## B. Data and integration

| Source | Edition | Scope and honest limit | Status |
|---|---|---|---|
| **IEC 61968-6** *Interfaces for maintenance and construction* | **2015-07, Ed. 1.0** | **The only standardised work/maintenance information model in either commodity.** Cl. 4.2 reference components — GINV MAI CON DGN **SCHD** FRD AM SIM NE TCM MR&C CS HR MM FIN — are the product-neutral system vocabulary. Cl. 5 payloads: WorkRequest, ServiceOrder, MaintenanceOrder. Annex A verbs. **Limit: it standardises what is exchanged between systems, not how work is scheduled or executed.** | Scope and cl. 4 `clause-verified` |
| **IEC 61968-11** CIM extensions for distribution | 2013, Ed. 2.0 | The `Work` package: `BaseWork`, `Work`, `WorkTask`, `WorkActivityRecord`, `WorkAsset`, `WorkLocation`, `MaterialItem`, `Tool`, `Vehicle`, and the WorkKind/WorkStatusKind/WorkTaskKind enums. **There is no `WorkOrder` class** — it is `Work` plus `workOrderNumber`. | `verified` from published CIM renderings |
| **IEC 61968-4 / -9 / -3 / -1** | 2019 / **2024 Ed.3** / 2021 / 2020 | Records and asset management; meter reading and control (Ed. 3 extends to gas and water metering, and is retitled *Enterprise business function interfaces for utility operations*); network operations; interface architecture. | `clause-verified` |
| **PODS** Pipeline Open Data Standard | PODS 7 / **7.03 Utility Network + APR, 2024-04-15** | Gas asset data model. Covers distribution as well as transmission. Has ACTIVITY, INSPECTION_RANGE, PHYSICAL_INSPECTION, REPAIR. **No work order, work task, maintenance or crew entities** — it records work done, it does not model the work item. | `verified` from the PODS 7 conceptual diagram |
| **UPDM** Utility and Pipeline Data Model (Esri) | **2026** | Gas distribution and transmission, DOT-reporting aligned. `P_ExcavationDamage` for CGA DIRT, CP inspection classes, ASTM F2897 barcodes. Same limit as PODS on work entities. **APDM is retired — do not cite it.** | `verified` from release notes |
| **MultiSpeak** (NRECA/CES) | **V5.0, 2015-02-18** (5.0.7 model 2017) | Electric cooperative integration. Does define work management interfaces. **No confirmed gas profile** — the "increasingly gas and water" line is an applicability claim, not a profile. Effectively dormant since 2021. IEC 61968-14 CIM↔MultiSpeak mapping is under development, not finished. | `consensus` |

**Do not cite:** GITA (dissolved 2021). PIDX (commercial B2B only). ISO 15926 and ISO/TC 67
(process plants and upstream, not distribution work).

---

## C. Field service management — read this before specifying 3.0, 4.0 or 10.0

**FSM is not a standards domain.** No ISO, IEC, CEN/EN, ANSI, BSI or national standard has
field service, mobile workforce management or service dispatch as its subject. Checked
against the ISO catalogue, ICS 03.080.x, CEN/TC 319, CEN/TC 348, BSI, IEEE and ANSI.
Nothing. State this plainly in the reference rather than padding a citation list.

Coverage of this space is split three ways, and each part has a real anchor:

| Question | Anchor |
|---|---|
| **What is exchanged** | IEC 61968-6 cl. 4.2 — **SCHD "Work Scheduling and Dispatching"** and **FRD "Field Recording"** are named, defined functional components in a published IEC standard, in this exact domain. Mobile Workforce sits inside FRD; Crew Composition is a named data flow. This is the closest thing to a standards basis for FSM that exists. |
| **What is measured** | EN 15341 **O&S9–O&S22** Planning and Control and **O&S23–O&S28** Productivity Effectiveness; SMRP 5.4.3/5.4.4 Schedule Compliance, 5.5.x resourcing ratios, **5.6.1 Wrench Time**. |
| **What is legally constrained** | OSHA — see section F. Job briefing, information transfer, qualified person, minimum approach distance, enclosed-space permits and excavation competent person are all **dispatch-gating process constraints**, not just PPE rules. |

**The actual process of scheduling, dispatching and executing field work is left entirely
to vendors and practitioner convention.** Where a specification needs it, the field is
`judgment` and says so.

**ISO/IEC 20000-1:2018** cl. 8 may be cited as a **labelled structural analogue** for the
intake-and-commitment layer only — 8.3.3 service level management, 8.4.2 demand
management, 8.4.3 capacity management, 8.6.1 incident management, 8.6.2 service request
management. The label is mandatory: say in the text that it is an IT service management
standard used as a structural reference, not as domain authority. It abstracts away
travel, geography, credential gating, safety envelopes, parts on a truck, connectivity
and customer presence — everything that makes field work hard. **Never cite it for
execution, scheduling or dispatch.**

**ITIL 4 is a proprietary commercial framework owned by PeopleCert, not a standard.** It
may be named as prevailing industry practice. It is never normative.

**Do not cite:** Field Service USA / WBR conference material, Aberdeen sponsored research,
TSIA except as named subscription research with a date, AFSMI (status unconfirmed),
"wrench time" as if standardised (define it yourself and attribute to SMRP 5.6.1).

---

## D. Utilities — cross-commodity

| Source | What it gives | Status |
|---|---|---|
| **EPRI** | The electric research body. Program 224 integrated asset management; Utility Digital Worker Collaborative; historic work-management reports (e.g. TR-109734). Largely member-gated. **EPRI has NOT published a work-identification taxonomy** — its public capability model defines Work Management in one sentence about estimating, scheduling and dispatching crews. | `consensus`, member-gated |
| **EPRI Utility Business Capability Model** | Public HTML browser, 18 capability classes. A *capability* model, not a process model. Useful as a cross-reference axis. | `consensus` |
| **Common Ground Alliance Best Practices** | **v21.0 verified** (v22.0 announced, date unconfirmed). ~164 practices. The 811 one-call process. **Genuinely cross-commodity**, and CGA BP 3-16 is the only publicly available consensus-defined minimum content set for a work-demand record in this whole space. Relevant to 1.0 and 8.0. | `consensus` |
| **ISO 55001:2024** | The only commodity-neutral asset management anchor. | `clause-verified` |

---

## D-bis. Design, estimating, authorisation and permits — added Round 1, 2026-08-29

Found while specifying category 2.0. Binding on all platforms from now on.

### Cost estimating

| Source | Edition | Use for | Status |
|---|---|---|---|
| **AACE International RP 96R-18** *Cost Estimate Classification System — as applied in EPC for the Power Transmission Line Infrastructure Industries* | Rev. 2020-08-07 | Estimate classes 1–5 against maturity of project definition, with accuracy ranges. **It says in cl. 2 that it applies to distribution as well as transmission.** Excludes substations — use 18R-97 for those. Also addresses the 30/60/90 percent design-review gate model directly. | `consensus` |
| **AACE RP 97R-18** *…Pipeline Transportation Infrastructure Industries* | Rev. 2020-08-07 | The gas equivalent. Note it carries **no** transmission/distribution equivalence sentence, so it is a reasonable but not explicit fit for distribution mains. | `consensus` |
| **AACE RP 17R-97** (generic parent), **34R-05** Basis of Estimate, **31R-03** Reviewing/Validating/Documenting the Estimate, **40R-08** Contingency, **68R-11** Escalation, **119R-21** Accuracy Range and Contingency, **10S-90** Cost Engineering Terminology (rev. 2026-06-11) | — | Method for each. | `consensus` |
| **ASTM E2516-11(2024)** *Standard Classification for Cost Estimate Classification System* | Reapproved 2024 | The one actual consensus **standard** in this space. Cross-references AACE. | `clause-verified` |
| **ISO 21502:2020** | 2020 | cl. **7.7 Cost management** (7.7.2 estimating, 7.7.3 budget, 7.7.4 controlling), cl. **7.10 Change control**, cl. **6.6.5 Managing the start, progress and close of each work package**. | `clause-verified` |

**Cite AACE as guidance, never as a standard.** RP 17R-97 §1 says so itself: *"This document is intended to provide a guideline, not a standard."* No AACE RP is ANSI-recognised; the only ANSI link is a 1972 historical reference. **Contingency and escalation values are firm judgment** — the RPs give method, not numbers.

### Compatible units and the accounting substrate

**"Compatible unit" has exactly one international-standard mention.** IEC 61968-6:2015 cl. **4.2.5 "Design"**, verbatim: *"A design is created by an engineer or work planner using the Design and Estimation System (DGN). Designs can be made up of individual line items or by a set of 'Compatible Units' or CUs. Line items and Compatible Units are associated with a Design Location which is associated with the Location object in the CIM."* Everything else about CU practice is firm judgment — **the catalogue's content has no authority.**

The accounting concept underneath it is fully citable:

- **18 CFR Part 101** (FERC USoA, electric) **Electric Plant Instruction 10(A)**: *"Each utility shall maintain a written property units listing for use in accounting for additions and retirements of electric plant and apply the listing consistently."* — the regulatory hook for a CU catalogue. FERC requires the listing to exist, not what is in it.
- **EPI 11 "Work Order and Property Record System Required"**: all construction and retirements recorded by work orders; maintenance costs segregated.
- **EPI 10(C)(3)** the betterment test — the capital-versus-expense determination.
- **EPI 4(B)**: *"The addition to direct construction costs of arbitrary percentages or amounts to cover assumed overhead costs is not permitted."*
- Definitions **34** retirement unit and **18** minor item of property.
- **18 CFR Part 201** (gas) is word-for-word parallel.
- **Scoping caveat that must be stated:** Part 101 binds FPA public utilities, Part 201 binds NGA natural gas companies. Neither reaches a state-regulated LDC directly — **states adopt them** (e.g. 220 CMR 50.00 in Massachusetts reproduces the work-order text).
- **7 CFR 1767.16(j)/(k)** and **7 CFR 1767.41 "Work Order Procedures"** (staking sheets, RUS Form 219) for RUS borrowers. RUS uses **"record unit"**, and *"Labor and overhead estimated by using standard record unit costs"* is the closest regulatory language to CU-based estimating anywhere in the CFR.

### Design process

- **ISO 9001:2015 cl. 8.3** is the correct process anchor: 8.3.1 general, 8.3.2 planning, 8.3.3 inputs (must consider statutory and regulatory requirements and codes of practice), 8.3.4 controls (**review, verification, validation** as distinct activities), 8.3.5 outputs (including acceptance criteria), **8.3.6 changes** (identify, review, control, and retain the **authorization of the changes**). ⚠️ **Edition 6 is at stage 60.00, expected September 2026** — date-stamp the citation.
- **7 CFR Part 1724** is a real, mandatory, public design-*process* regulation for RUS borrowers and is far stronger than NESC for this: **1724.51** design requirements, **1724.53** preparation of plans and specifications (and **1724.53(b)(1)** enumerates package contents by asset class), **1724.54** RUS approval gate, **1724.32** inspection and certification of work order construction.
- **NESC (ANSI/IEEE C2-2023) has no design-review, approval or documentation requirement.** It is safety criteria. Do not cite it for design process.
- **49 CFR 192 Subpart B is the design of pipe, not a design process.** § 192.127 is the only design-records rule and it is **gas transmission only**, post-July-2020 installs.
- ASME **B31.8-2025** and **B31.8S-2025** are current, but 49 CFR 192.7 incorporates the **2018** editions and only for named purposes. State which you mean.

### Authorisation and change control

- **ISO 55001:2024 cl. 6.3 "Planning of changes" together with cl. 8.2 "Control of change".** The risk-assessment requirement **moved out of 8.2 into 6.3** in the 2024 edition — citing 8.2 alone cites an emptied clause.
- **ISO 9001:2015 cl. 8.5.6** control of changes; cl. 8.3.6 design changes.
- **49 CFR 192.13(d)** is the best management-of-change element list anywhere: *"reason for change, authority for approving changes, analysis of implications, acquisition of required work permits, documentation, communication of change to affected parties, time limitations, and qualification of staff."* ⚠️ **Onshore gas transmission only**, effective 2024-02-26. **DIMP (§192.1007) has no MOC element**, so for gas distribution MOC is voluntary practice — API RP 1173 is the reference and PHMSA ADB-2025-01 only encourages it.
- **7 CFR 1710.250(e)**: RUS facilities must be approved and receive environmental clearance **before the start of construction**.

### Permits and prerequisites

- **CGA Best Practices v22.0, March 2026** — free PDF, 160+ practices. Chapter 2 Planning and Design: **2-2** gathering information for design, **2-3** identifying existing facilities, **2-6** follow codes and operator standards, **2-14** subsurface utility engineering, **2-16** project coordination. Chapter 3: **3-15** 811 centre accepts design requests, **3-16** locate request and its minimum fields. Chapter 5: **5-1** locate request with the statutory waiting window, **5-3** locate reference number, **5-23** updates, **5-35** large/complex project request (new in 22.0).
- **ASCE 38-22** *Standard Guideline for Investigating and Documenting Existing Utilities* — named by CGA 2-14 as the governing SUE standard.
- **49 CFR 192.614** damage prevention. ⚠️ Read it correctly: it obliges the operator **as facility owner**, not as excavator. The call-before-you-dig duty is **state one-call statute**, not Part 192.
- **MUTCD 11th Edition, December 2023, with Revision 1 incorporated, December 2025**, per 23 CFR 655.601(d)(2)(i); **Part 6 Temporary Traffic Control**, Part 8 railroad crossings. The **permit itself** is state or municipal and is not federally standardised.
- **USACE Nationwide Permits 2026** (effective 2026-03-15, expiring 2031-03-15): NWP 12 gas pipelines, NWP 57 electric utility lines, NWP 58 other utility lines, NWP 3 maintenance, NWP 14 linear transportation. **40 CFR 122.26(b)(15)(i)** small construction ≥1 acre, and note its exclusion: *"Small construction activity does not include routine maintenance that is performed to maintain the original line and grade, hydraulic capacity, or original purpose of the facility."* **40 CFR Part 112** SPCC is facility-level, not job-level.

### Three verified negatives for this category

1. **No standard specifies what a work package must contain.** EN 13460:2009 Annex B is **informative** and paywalled with no public content; ISO 14224 cl. 9.6 is maintenance-record data, not package content; IEC 61968-6 is a data model. The only prescriptive content list is **7 CFR 1724.53(b)(1)**, and that binds RUS borrowers only. Work-package content is `judgment`.
2. **No consensus practice exists for permit management as a process.** CGA covers 811 comprehensively and nothing else. Obtaining, tracking, expiring and closing out road-opening, railroad, environmental and traffic permits is `judgment`.
3. **CII Advanced Work Packaging is a consortium best practice, not a standard**, and its implementation resources are members-only. Definitions are public; content specifications are not.

---

## D-ter. Closure, cost settlement, unitisation and as-built — added Round 2, 2026-08-29

Category 5.0's sources, read for round 2. The pattern here is the reverse of design: the
accounting side is heavily prescribed and the field-record side is barely prescribed at all.

### Closure and verification

| Source | Use it for | Status |
|---|---|---|
| **EN 17007:2017 cl. 6.5.8 ACT.7** *Finalise the maintenance tasks* | The closure process itself. This is the anchor for 5.1 and it is the last of the seven ACT processes. | `verified` |
| **ISO 9001:2015 cl. 8.6** *Release of products and services*, **cl. 8.7** *Control of nonconforming outputs* | Verification before release, and the rework path at 5.1.3. Titles confirmed; bodies paywalled. | `clause-verified` |
| **49 CFR 192.605(b)(8)** | *"Periodically reviewing the work done by operator personnel to determine the effectiveness, and adequacy of the procedures used in normal operation and maintenance."* A federal requirement to review completed work — it makes 5.1.2 a duty for gas, not a preference. | `regulation` |

### Cost settlement and unitisation — heavily prescribed

| Source | Use it for | Status |
|---|---|---|
| **18 CFR 101** Electric Plant Instruction 3 | Components of construction cost — what may be charged to a work order. | `regulation` |
| **18 CFR 101** EPI 4(B) | Overhead may not be an arbitrary percentage added to direct construction cost. Already used at 2.3.3; it binds again at settlement. | `regulation` |
| **18 CFR 101** EPI 10(A), 10(C), Definitions 18, 34 | Additions and retirements, the betterment test, retirement unit and minor item. The determination is made at 2.2.5; 5.3 executes it against actuals. | `regulation` |
| **18 CFR 101** EPI 11, Definition 8 | Work order requirement and the **continuing plant inventory record**. | `regulation` |
| **18 CFR 125.3 Item 17(a)(b)(c)** | Construction work in progress ledgers, work order sheets for plant additions, and authorisation records: **5 years after clearance to plant account**, provided continuing plant inventory records are maintained; otherwise 5 years after the plant is retired. | `regulation` |
| **18 CFR 125.3 Item 16(b)** | The continuing plant inventory ledger itself: **25 years**. Note the asymmetry — the work order may go at 5 years, the property record may not go for 25. | `regulation` |
| **7 CFR 1767** | RUS accounting for electric borrowers; adopts the FERC system with additions. | `regulation` |

### As-built and asset records — barely prescribed, and asymmetric

| Source | Use it for | Status |
|---|---|---|
| **49 CFR 192.605(b)(3)** | *"Making construction records, maps, and operating history available to appropriate operating personnel."* This is the closest thing to a federal as-built duty for gas, and note what it requires: availability to operations, not accuracy. | `regulation` |
| **49 CFR 192.709(a)** | The date, location and description of each repair made to **pipe** must be retained **for as long as the pipe remains in service**. A permanent record obligation — but transmission only. | `regulation` |
| **49 CFR 192.709(b), (c)** | Other repairs, 5 years. Patrols, surveys, inspections and tests, 5 years or until the next one, whichever is longer. | `regulation` |
| **49 CFR 192.13(c)** | *"Each operator shall maintain, modify as appropriate, and follow the plans, procedures, and programs that it is required to establish under this part."* | `regulation` |
| **49 CFR 192.607** | Material verification for onshore steel **transmission**. Records-driven, and the reason traceable-verifiable-complete language entered the industry. Not a distribution requirement. | `regulation` |
| **ASCE 38-22** | Quality levels for subsurface utility location. Already in D-bis for survey at design; it applies again at 5.4.2 for as-built capture. | `clause-verified` |
| **IEC 61968-6 cl. 4.2** FRD *Field recording* | The component that owns as-built capture. | `clause-verified` |

### What is genuinely not standardised here — say so

1. **There is no federal as-built positional accuracy requirement for gas distribution or
   for electric anything.** 192.605(b)(3) requires records be *available*, not that they be
   correct to a tolerance. Accuracy standards are the operator's, sometimes a state's.
2. **There is no federal as-built requirement for electric distribution at all.** 16 U.S.C.
   824o excludes local distribution, and NESC sets no record-keeping duty. This is the same
   asymmetry as section E and it runs the whole length of category 5.0.
3. **Nothing standardises the work-order closure state model.** Whether closure is one
   state or four, and what may reopen a closed order, is the operator's.
4. **Nothing standardises unitisation mechanics.** FERC says what a retirement unit is and
   that additions and retirements must be recorded; how a completed job is broken into
   units against actual cost is an operator method.

## D-quater. Vegetation management — added Round 2, 2026-08-29

Found missing when Grok specified category 7.0. The pack had the state inspection
intervals and nothing on method, finish or worker safety.

| Source | Edition | Use it for | Status |
|---|---|---|---|
| **ANSI A300** *Tree Care Operations — Tree, Shrub, and Other Woody Plant Management — Standard Practices* | multi-part; **Part 7 Integrated Vegetation Management, 2018** | The industry specification for METHOD and FINISH: pruning, IVM, and what a prescription means. ANSI-accredited, TCIA secretariat. **Not incorporated by reference into any federal rule** — it is consensus, not law, and binding only where a state or a contract adopts it. | `consensus` |
| **ANSI Z133** *Arboricultural Operations — Safety Requirements* | **2017** | Worker safety for tree work. Same status: ANSI-accredited consensus, not federally incorporated. | `consensus` |
| **29 CFR 1910.269(r)** *Line-clearance tree trimming operations* | current | The FEDERAL rule, and the one that actually binds. Note OSHA's defined terms are **line-clearance tree trimmer** and **qualified employee** — not "ISA Certified Arborist" or "qualified line-clearance arborist", which are industry terms. Use OSHA's words in a specification. | `regulation` |
| **29 CFR 1910.269 Tables R-5 to R-8** | current | Worker minimum approach distances. **These are not vegetation clearance distances** and must never be quoted as though they were. | `regulation` |
| **NERC FAC-003** *Transmission Vegetation Management* | current | Cite it only to say what it is NOT. It applies to the bulk electric system; 16 U.S.C. 824o excludes local distribution. There is **no federal distribution vegetation clearance distance at all**. | `clause-verified` |

**What is genuinely not standardised.** Hazard-tree and danger-tree identification criteria;
remote survey by LiDAR, satellite or drone; growth and encroachment modelling; notice
content to landowners; refusal handling; completion-evidence content; audit sample size;
and vegetation cause codes. Herbicide and pesticide law is state and is outside this pack.
Say so rather than inventing a practice.

**APQC has no vegetation management process.** The only touch in the whole framework is
10.4.5 waste and hazardous goods (pcf_id 16970). A specialised category with no APQC
counterpart is a finding about APQC's coverage of utilities, not about this model.

## E. The gas / electric asymmetry — the most important thing in this pack

The common assumption is that electric is better standardised. **It is the reverse for
work management.** Gas is stronger on five of nine capability areas, and those five are
precisely what a work-management reference is built from.

| Capability | Stronger | Why |
|---|---|---|
| Prescriptive inspection/maintenance intervals | **GAS, decisively** | 49 CFR 192 Subpart M. Electric distribution has **no federal equivalent at all.** |
| Integrity management programme | **GAS, decisively** | 49 CFR 192 Subparts O and P (DIMP §§192.1001–1015). Electric distribution: nothing. |
| Personnel qualification | **GAS, decisively** | 49 CFR 192 Subpart N + ASME B31Q-2025. No federal qualification requirement exists for electric distribution workers. |
| Emergency response | **GAS** | 49 CFR 192.615 and 192.605. Electric distribution: state only. |
| Leak/fault classification | **GAS** (consensus, not law) | ANSI/GPTC Z380.1 G-192-11. Electric has no analogue. |
| Reliability/performance measurement | **SPLIT** | Electric has the better *method* (IEEE 1366-2022) but it is voluntary federally; gas has **mandatory** federal reporting of four DIMP measures under §192.1007(e)/(g) and §191.11. |
| Data model — work | **ELECTRIC** | IEC 61968-6 is the only work model in either commodity. |
| Data model — asset and inspection | **GAS** | PODS 7 and UPDM 2026 are actively maintained and DOT-aligned; IEC 61968-6 is a single 2015 edition at its stability date. |
| Asset condition assessment | **NEITHER** | No IEEE, NEMA or ISO standard for distribution asset condition assessment or health indexing in either commodity. Health-index literature is academic and CIGRE-conference, not standardised. Only sector-neutral anchor is ISO 55001. |

**The cause.** 16 U.S.C. 824o defines the bulk-power system and states *"The term does not
include facilities used in the local distribution of electric energy"*, and §824o(i)(1)
limits the ERO to reliability standards *"for only the bulk-power system."* Electric
distribution sits outside the federal regime by statute.

**The one-line illustration.** NESC (ANSI/IEEE C2-2023) Rule 214A2: *"Lines and equipment
shall be inspected at such intervals as experience has shown to be necessary."* Against
49 CFR 192.721: *"at intervals not exceeding 4 1/2 months, but at least four times each
calendar year."*

**The correct narrow claim**, which replaces the earlier over-broad one: *electric has a
work/maintenance message standard and gas has none; gas has stronger asset and inspection
data models; and gas is far more heavily regulated on everything a work-management
reference is built from.*

---

## F. Gas distribution

| Source | Edition | Use for | Status |
|---|---|---|---|
| **49 CFR Part 192** | current eCFR | The prescriptive spine. Interval grammar: *"at intervals not exceeding X months, but at least once each calendar year"* — **both bind.** Annual=15mo, 3yr=39mo, 5yr=63mo, quarterly=4½, semiannual=7½, 2-monthly=2½. Key sections: **192.605** O&M procedural manual · **192.614** damage prevention (no numeric interval) · **192.615** emergency plans · **192.616** public awareness (no interval in the CFR) · **192.465** CP monitoring and remediation · **192.481** atmospheric corrosion (note **(d)**: a prior finding shortens 63→39 months) · **192.703(c)** *"Hazardous leaks must be repaired promptly"* — the entire federal leak requirement · **192.721** patrolling (numeric intervals apply **only** to mains subject to physical movement or external loading) · **192.723** leakage surveys (three cases: business district 15mo, outside 63mo, cathodically unprotected 39mo) · **192.739/743** regulator stations · **192.747** valves · **192.749** vaults · **Subpart N** 192.801–809 operator qualification · **Subpart P** 192.1001–1015 DIMP, incl. 192.1007 seven elements and 192.1013 deviation. | `regulation` |
| **ANSI/GPTC Z380.1** | **2025 Edition** | ANSI-accredited consensus, AGA secretariat. **G-192-11** leak grading §5.6 and Tables 3a–3c; §5.8 temporary mitigation; §5.9 follow-up; §6.1 leak record data set. Guide material on **192.605** (the closest thing in gas to a published O&M *process* reference), 192.614, 192.615, 192.703. **NOT incorporated by reference into Part 192** — it does not appear in the §192.7 IBR list. Binding only where a state adopts it. **Say both, every time.** | `consensus` |
| **API RP 1173** *Pipeline Safety Management Systems* | 1st ed. 2015-07, reaffirmed R2023 | **The most process-shaped citable document in the gas sector.** Ten elements incl. Operational Controls, Risk Management, Competence/Awareness/Training, Emergency Preparedness, Documentation. Plan-Do-Check-Act. **Voluntary** — PHMSA Advisory Bulletin 90 FR 13658 (2025-03-25) "strongly encourages" adoption and states advisory bulletins create no obligations. | `consensus` |
| **ASME B31.8 / B31.8S** | current | Gas transmission and distribution piping; managing system integrity. The authority behind DIMP/TIMP. | `clause-verified` |
| **ASME B31Q** | **2025** | Pipeline personnel qualification programme requirements. Pairs with Subpart N. | `clause-verified` |
| **AMPP SP0169** (formerly NACE) | current | External corrosion control on underground metallic piping. Authority behind category 8's corrosion groups. | `clause-verified` |
| **49 CFR Part 199** | current eCFR | **Gas-only** drug and alcohol testing for covered employees performing operations, maintenance or emergency response. Random testing ≥50% annually. Electric utilities are not covered. | `regulation` |
| **AGA** | — | Performance benchmarking reports (latest covers 2019–2021, published 2023-04) are **free and public**. Peer Review Program (since 2015) is process-shaped; protocols are member material. Operations Best Practices Program. **GEOP series volumes date 1985–2004 — two decades stale, cite with care.** | `consensus` |
| **GTI Energy / OTD** | — | The functional gas analogue of EPRI, **with a more restricted publication model**. Many OTD reports free on request. | `consensus` |
| **NFPA 54 / 58** | current | National Fuel Gas Code; LP-Gas Code. | `clause-verified` |
| **PHMSA public material** | — | DIMP inspection forms, DIMP guidance (2013), SHRIMP plan tool. Free. No electric analogue exists. | `regulation`/`consensus` |

**Not in force, cite only as history:** PHMSA Gas Pipeline Leak Detection and Repair final
rule — sent to the Federal Register 2025-01-16, withdrawn under the regulatory freeze
before publication. It would have codified leak grading federally. It did not.

**Training bodies, not standards publishers:** MEA Energy Association (EnergyU, 430+
courses covering 49 CFR 192/195 and ASME B31Q), NGA, SGA.

---

## G. Electric distribution

| Source | Edition | Use for | Status |
|---|---|---|---|
| **IEEE 1366** | **2022** | SAIFI, SAIDI, CAIDI and the Major Event Day 2.5-beta method. The definitional authority for distribution reliability. **Voluntary federally** — EIA-861 lets non-calculating entities skip the schedule. | `clause-verified` |
| **NESC — ANSI/IEEE C2** | **2023** (published 2022-08-01) | Construction, clearance and safety for supply and communication lines. Governs joint-use pole space. **Rule 214A2 is the inspection provision and is deliberately non-prescriptive.** | `verified` for Rule 214A2 |
| **NERC** | current | FAC, PRC and TPL families. **Bulk power system only** — largely out of scope for distribution work, except where a utility's transmission assets are in scope. CIP-013 supply chain risk for 16.0. | `clause-verified` |
| **State inspection rules** | — | This is where electric distribution intervals actually live, and the variation is dramatic. **California CPUC GO 165** (adopted 1997-03-31, revised 2017-12-14 by D.17-12-024) — Table 1 intervals by facility type and urban/rural, wood poles intrusive 10 years. **California CPUC GO 95 Rule 35** *Vegetation Management* is the separate and equally important one — radial clearances at Table 1 Cases 13 and 14, mature tree exemptions at 13E and 14E, guidelines at Appendix E. GO 165 is inspection; GO 95 Rule 35 is clearance. *Added 2026-08-29 — Grok found the omission.* **Pennsylvania 52 Pa. Code § 57.198** — vegetation is a **4-to-8 year** statewide minimum inspection and treatment cycle for distribution facilities at (n)(1), NOT a fixed 8 years, plus a plan under (f) that must include a programme for maintaining clearances; poles 12yr, OH lines 2yr, substations 5 weeks. *Corrected 2026-08-29 — Grok found this reading the regulation for category 7.0.* **Ohio OAC 4901:1-10-27** (eff. 2024-04-08) — distribution once every 5 years, substations 12×/yr at ≤40 days. **New Jersey N.J.A.C. 14:5-8.6** — requires a programme but **sets no intervals at all.** Name the state exemplar; never imply a national rule. | `regulation` |
| **FERC Uniform System of Accounts / Form 1** | current | Capital versus expense treatment and unitisation. Relevant to 5.0. | `clause-verified` |
| **IEEE 1782** | 2022 | Collecting and categorising distribution interruption event information. Relevant to 9.0. | `clause-verified` |
| **IEEE 1808** | 2024 | Transmission line inspection and maintenance data. **Transmission only — no distribution equivalent exists.** | `clause-verified` |
| **IEEE 516** | 2021 | Maintenance methods on energised lines — work *methods*, not a programme standard. | `clause-verified` |
| **EEI** | — | Mutual assistance and business continuity (relevant to 9.0 storm work). Employment aptitude batteries (CAST, POSS, MASS, TECH) if 14.0 covers selection. No process standard. | `consensus` |

**Do not claim:** a NEMA standard for distribution asset inspection (searched, none found;
absence not proven). IEEE 493 (edition and scope unverified — do not cite).

---

## H. Safety regulation — real, enforceable, and it constrains process

These are among the most precisely citable items available, and they are **process
constraints on dispatch and execution**, not merely PPE rules.

| Source | Scope | Notes |
|---|---|---|
| **29 CFR 1910.269** | *"the operation and maintenance of electric power generation, control, transformation, transmission, and distribution lines and equipment"* — **electric only** | **(a)(3)** host/contract employer information transfer · **(c) job briefing** before each job · **(d)** hazardous energy control for generation · **(e)** enclosed spaces · **(f)** excavations · **(l)** minimum approach distance · **(m)** deenergizing for T&D. Covers line-clearance tree trimming. |
| **29 CFR 1926 Subpart V** | Construction of electric power T&D lines | Harmonised with 1910.269 by the 2014 rule (**79 FR 20696**, eff. 2014-07-10); complying with 1910.269 is deemed compliance. **The split is construction vs O&M, not two regimes.** |
| **29 CFR 1910.147** LOTO | **Excludes** installations under the exclusive control of electric utilities for generation, transmission and distribution — §1910.147(a)(1)(ii)(C) | **The asymmetry runs the other way here.** Electric utility T&D uses 1910.269(d) and (m); complying with 1910.147 does **not** satisfy 1910.269(m). **Gas utilities are not excluded, so 1910.147 applies to gas distribution work.** Do not list LOTO as a shared standard without this. |
| **29 CFR 1910.146** permit-required confined spaces | General industry | For utility work, **1910.269(e) enclosed spaces** is the distinct and less onerous regime. Construction work uses **1926 Subpart AA**. Frequent misattribution — get the right one. |
| **29 CFR 1926 Subpart P** | Excavations, §§1926.650/651/652 | Gas, water and underground electric. **Competent person** requirement gates assignment. 1910.269(f) also addresses excavation for utility O&M. |
| **NFPA 70E** | Electrical safety in the workplace | **Cite the edition explicitly.** 2024 remains the edition in general use; the 2027 (14th) edition was issued around the NFPA Standards Council meeting of 2026-08-18/20 — verify issuance and effective dates with NFPA before publishing. ANSI-approved standard, **not** an OSHA regulation; OSHA cites it as recognised practice under the General Duty Clause. |

---

## I. What is genuinely not standardised — say so, do not invent

Recording these honestly is more valuable than a padded citation list. Each has already
been tested against primary sources.

1. **Field service management as a discipline** — no standard anywhere.
2. **Scheduling, appointment booking and resource optimisation** — no standard. ISO 30409:2016 is strategic workforce planning, not rostering or dispatch; do not stretch it.
3. **Offline mobile behaviour, sync conflict resolution, field data capture, electronic forms** — entirely vendor-defined.
4. **"Wrench time"** — not defined in EN 15341, EN 13306 or EN 17007. Only SMRP 5.6.1 defines it, and that is a member-gated professional-society best practice.
5. **A work request content model spanning gas and electric** — none. IEC 61968-6 is closest and is electric-only. The two public consensus content sets are domain-specific: CGA BP 3-16 for locate requests, GPTC G-192-11 §6.1 for leak records.
6. **A gas work/work-task information model** — none. PODS and UPDM model the record of work done, not the work item.
7. **Electric distribution inspection intervals** — no federal layer; state by state, and some states set none.
8. **Operator qualification requalification intervals** — entirely operator-set under §192.805(g).
9. **"Business district"** — undefined in Part 192 despite being the most consequential discriminator in leak survey and patrol scheduling. It comes from the operator's §192.605 manual.
10. **Distribution asset condition assessment / health indexing** — no standard in either commodity.
11. **Leak grades as federal law** — they are not. §192.703(c) is the whole federal text.
12. **Adoption levels for any of this** — existence, scope and currency were verified; how many utilities actually implement them was not.

---

## J. Worth buying — converts `clause-verified` to `verified`

Roughly €60–120 each from a national body (SIS, EVS, NEN; avoid BSI pricing):
**EN 17007:2017** (process profiles for COR.1, COR.2 and ACT.1–ACT.5 — the whole demand
chain, pp. 24–34) · **EN 13460:2009** (Annex B work order information items) ·
**EN 13306:2017** (cl. 7 and Annex E) · **EN 15341:2019+A1:2022** (cl. 12, O&S9–O&S22).
Also worth having: **ANSI/GPTC Z380.1-2025** and **SMRP Best Practices 7th Edition**
(free with SMRP membership).

---

## Section E — Joint use and third-party attachments (added 2026-08-29 for category 11.0)

**This category had no coverage in the pack at all, and that is not an oversight in the
pack — it is the finding.** Neither APQC PCF Utilities nor the GFMAM Asset Management
Landscape has a home for pole attachment work, which makes 11.0 the only category in the
model that no public framework reaches. Everything below was obtained for this round.

Federal law is unusually thick here, and it is *procedural* law: it prescribes the
timetable a utility must run its attachment process to, which is precisely the kind of
content the rest of this reference has to derive from consensus.

### E1 — The statute

| Source | Locator | What it establishes | Status |
|---|---|---|---|
| **47 U.S.C. 224** | (a)(4) | "pole attachment" is any attachment by a cable television system or provider of telecommunications service to a pole, duct, conduit or right-of-way owned or controlled by a utility | `regulation` |
| | (b)(1) | the FCC regulates rates, terms and conditions to be just and reasonable | `regulation` |
| | (c)(1)–(2) | **reverse preemption**: the FCC has no jurisdiction where a State certifies that it regulates pole attachments and considers the interests of subscribers | `regulation` |
| | (d)(1) | the cable rate floor: not less than the additional costs of providing pole attachments | `regulation` |
| | (e) | the telecommunications rate formula | `regulation` |
| | (f)(1) | a utility **shall** provide nondiscriminatory access | `regulation` |
| | (f)(2) | an **electric** utility may deny access on a non-discriminatory basis for insufficient capacity, safety, reliability or generally applicable engineering purposes | `regulation` |
| | (h) | written notice of intended modification | `regulation` |
| | (i) | an attacher does not bear the cost of rearranging or replacing its attachment where that is required by an **additional** attachment | `regulation` |

**224(c) is the single most important structural fact in this category.** Roughly half the
states have certified, and in those states the federal timeline below does not apply — the
state's does. Every process here therefore determines *which regime governs* before it
applies a number. No state regime is in this pack; naming one is `judgment`.

### E2 — The FCC rules, 47 CFR Part 1 Subpart J (read verbatim from the current eCFR)

| Locator | What it establishes | Status |
|---|---|---|
| **1.1403(a)** | duty to provide access; denial only on a non-discriminatory basis for insufficient capacity, safety, reliability or generally applicable engineering purposes, in writing with all supporting evidence | `regulation` |
| **1.1403(c)** | **60 days** written notice before removal, a rate increase, or modification other than make-ready, routine maintenance or emergency response | `regulation` |
| **1.1406(d)** | the maximum just and reasonable rate formulas — (d)(1) cable, (d)(2) telecommunications (higher of two), (d)(3) conduit | `regulation` |
| **1.1407** | remedies: prescribe a rate, terminate or substitute a term, order a refund with interest, order access within a specified time | `regulation` |
| **1.1408(b)** | **modification cost allocation**: borne by all parties that obtain access as a result of the modification and all parties that directly benefit, shared proportionately | `regulation` |
| **1.1409(a)–(d)** | unusable-space apportionment at two-thirds of an equal share; rebuttable presumptive attaching-entity averages of **3** (non-urbanized, under 50,000) and **5** (urbanized) | `regulation` |
| **1.1410** | rebuttable presumptions: attachment **1 ft**, usable space **13.5 ft**, unusable space **24 ft**, pole height **37.5 ft** | `regulation` |
| **1.1411** | the access timeline — see E3 | `regulation` |
| **1.1412(a)–(c)** | contractor lists for self-help and simple work; minimum qualifications, including agreeing to follow **NESC** guidelines where the utility publishes none, and OSHA Qualified and Competent Person rules | `regulation` |
| **1.1415** | the Rapid Broadband Assessment Team, and the Accelerated Docket route for disputes alleged to delay broadband deployment | `regulation` |
| **1.1416** | **overlashing**: no prior approval for an existing attacher overlashing its own wires or a permitted third party; no more than **15 days** advance notice; a utility may not block an overlash over another attacher's preexisting violation | `regulation` |

### E3 — The 47 CFR 1.1411 timeline, verbatim

Order sizes, at **1.1411(a)(4)–(5)**: a **Mid-Sized Order** is greater than the lesser of
300 poles or 0.5% of the utility's poles in a state, up to the lesser of 3,000 or 5%. A
**Large Order** runs from there to the lesser of 6,000 or 10%. Above that, 1.1411(h)(4)
requires good-faith negotiation of the timing and no number applies.

| Stage | Locator | Standard | Mid-Sized | Large |
|---|---|---|---|---|
| Advance notice before submitting | (c)(1) | — | 15 days | 60 days |
| Meet and confer after advance notice | (c)(3) | — | — | within 30 days |
| Completeness determination | (d)(1)(i) | 10 business days, else **deemed complete** | same | same |
| Resubmitted application deemed complete | (d)(1)(ii) | 5 business days | same | same |
| Grant or deny on the merits | (d)(2) | 45 days | 60 days | 90 days |
| Survey | (d)(3)(i) | 45 days | 60 days | 90 days |
| Estimate after survey | (e) | 14 days | 14 days | 29 days |
| Make-ready **in** the communications space | (f)(1)(ii) | 30 days | 75 days | 120 days |
| Make-ready **above** the communications space | (f)(2)(ii) | 90 days | 135 days | 180 days |

Other numbers read from the same section: a **3 business day** notice of field inspection
(d)(3)(ii); cyclical pole inspection reports on written request within **10 business days**
(d)(4)(i); a **15 day** warning where the utility knows it cannot meet the survey (d)(3)(i)
or make-ready (f)(4) deadline; the utility's **15 day** right of control above the
communications space (f)(2)(iv); an estimate withdrawable **14 days** after presentation
(e)(1); multiple requests within **30 days** treatable as one (h)(5).

**One-touch make-ready**, 1.1411(k): available for **simple** make-ready at the new
attacher's election, with a **15 day** merits review (30 Mid-Sized, 45 Large) and **15
days** prior written notice of the work. The utility may object that make-ready designated
simple is complex, and **that objection is determinative**.

**Self-help**, 1.1411(j): available for surveys, estimates and make-ready when the utility
misses its deadline — and **1.1411(j)(3) states that self-help is not available for pole
replacements.** That single sentence is why 11.5 exists as its own group.

**Cost, 1.1411(e)(4):** a utility **may not charge** a new attacher to bring poles,
attachments or third-party equipment into compliance where they were out of compliance
because of work performed by a party other than the new attacher before the new
attachment. Read with 1.1408(b) and 47 U.S.C. 224(i), this is the whole of the federal
cost-allocation rule for make-ready.

### E4 — Engineering and the physical envelope

| Source | Locator | Status | Note |
|---|---|---|---|
| **NESC (ANSI/IEEE C2-2023)** | Rule 235C vertical clearances between conductors at poles; Rule 238 supply/communication equipment clearances; Rule 250B combined ice and wind loading districts; Rule 224A1 qualified workers in the supply space; Rule 230E1 vertical clearance above ground | `clause-verified` | Rule numbers and subjects confirmed from the NRECA guide below, which cites the 2023 edition. **The body is paywalled and is not paraphrased anywhere in this category.** |
| **NRECA**, *Guide for the Application of Clearance Requirements on Joint-Use Poles*, Distribution Subcommittee Overhead Work Group, May 2025 | whole | `consensus` | Public. Establishes the **communication worker safety zone** — generally 40 in above the communication space — as the separation between communication and supply space. The 40 in figure is NRECA's and is cited as NRECA's, not as NESC's. |
| **29 CFR 1910.268** | Telecommunications | `regulation` | The standard that governs the attacher's own workers, distinct from 1910.269 for the utility's. |
| **29 CFR 1910.269(a)(3)** | host and contract employer information transfer | `regulation` | Applies to a contractor doing make-ready on the utility's structures exactly as it applies at 16.2.2. |

### E5 — What is NOT in the pack, and is therefore `judgment`

* **Every state joint use regime.** 47 U.S.C. 224(c) hands roughly half the country to state
  commissions and no state rule is held here. A process may say the regime must be
  determined; it may not state what any state's rule says.
* **Joint ownership ratios and net settlement.** Two-party pole ownership with periodic
  balancing is universal practice and no standard describes it.
* **Unauthorised attachment penalties and back-billing periods.** Contract and tariff.
* **Audit cycle length and sampling method.** No source states one.
* **Double-wood and stub-pole backlog targets.** No source states one.
* **Transfer notification exchanges.** A multi-party notification system is the norm and
  the reference names no product, per the product-neutrality rule.


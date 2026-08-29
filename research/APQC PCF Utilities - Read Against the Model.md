# APQC PCF Utilities read against the reference model

**Date** 2026-08-29 · **Platform** Claude · **Status** finding, no model change made

## What was read

Three files supplied to `Tim Evidence/` on 2026-08-29:

| File | What it is | How it is used |
|---|---|---|
| `K07220_Utilities_v721_vs_Utilities_v610_2025.xlsx` | APQC PCF **Utilities v7.2.1**, with a difference index against v6.1.0 | **The authority for structure and numbering.** Extracted to `build/eam/apqc_pcf_utilities.json` by `build/extract_apqc.py` — 2,073 elements, 14 categories |
| `Utilities Process_v722_March_2025.pdf` | APQC PCF **Utilities v7.2.2**, March 2025 | Cross-check only. Its two-column layout does not extract reliably |
| `K016808_..._Cross-Industry_Excel_Version_8.0.xlsx` | APQC PCF **Cross-Industry v8.0**, generated 2026-02-25 | Confirms the cross-industry framework has moved to 8.0 while **Utilities has not** — there is no Utilities v8.0 |

Every PCF ID cited below was checked to exist in both the v7.2.1 Excel and the v7.2.2
PDF, so the identifiers are stable across the two published versions.

## An erratum in the published v7.2.2 PDF

In the v7.2.2 PDF the **10.4 group header reads "Maintain productive assets (19238)"** —
repeating 10.3 — while listing the five disposal processes beneath it: 10952 Develop exit
strategy, 19258 Decommission productive assets, 10953 Perform sale or trade, 10954 Perform
abandonment, 16970 Perform waste and hazardous goods management. PCF ID **10940 "Dispose of
assets" appears nowhere in that PDF.** The v7.2.1 Excel has it correctly as 10.4.

This is a publication error, not a restructure. It is recorded here so that nobody later
"corrects" the model against it.

## Only two of fourteen categories carry utility content

APQC PCF Utilities is the cross-industry framework plus **10.0 Acquire, Construct, and
Manage Assets** and **14.0 Operate Utility Assets**. Those two are what this model can be
tested against; the other twelve are HR, IT, finance and the rest, and are the reason the
model has an enabling band rather than an attempt to cover them.

## The crosswalk

`build/make_apqc_crosswalk.py` → `build/eam/apqc_crosswalk.json`. Thirty-eight level-3
processes across the two utility categories, mapped by hand — a coverage claim a machine
guessed by string similarity is worth nothing.

| Status | Count | Meaning |
|---|---|---|
| covered | 12 | A model group or process does this work |
| partial | 6 | The model does part of it; the rest is named |
| **absent** | **8** | APQC has it and the model does not |
| scope | 12 | Deliberately outside a work-and-asset-management model, with the reason |

Twelve of the thirty-eight are corporate real estate, generation, water treatment and
network optimisation — genuinely outside scope. Of the twenty-six that are in scope,
**eight are absent and six are partial.**

## The eight absent processes, in order of how much they matter

### 1. 14.1.6 Perform planned network operation (19285) — the largest gap

Seven activities: submit outage switching and diversion plans (19286), approve or reject
the plan (19287), schedule planned network operations (19288), perform outage
notifications (19289), execute planned switching and diversions (19290), **co-ordinate
with maintenance and construction operations (19291)**, return the network to service
(19292).

The model consumes the result of this process and never performs it. `2.6.3 Validate
prerequisites before release` takes an isolation and clearance arrangement as an input
from network operations. `4.4.4 Confirm isolation and permit-to-work` checks one exists.
`9.3.2 Coordinate authorised isolation and switching` does it during *restoration*, which
is the unplanned case. Nothing plans, approves, schedules or executes switching for
**planned** work.

This is not a modelling nicety. Planned work on an energised network cannot start without
a clearance, the clearance has its own approval chain and its own lead time, and 29 CFR
1910.269(m) *Deenergizing lines and equipment for employee protection* and 1910.269(d)
hazardous energy control make the sequence a legal one. The model currently has a
regulated, lead-time-bearing process sitting in a field labelled "input".

### 2. 10.2.2 Perform utility network planning (19213)

Demand forecasting (19214), assess performance and capacity of current assets (19215),
network modelling (19216), protection design (19217), secondary systems design (19218).

The model's `3.1 Forecast demand and capacity` forecasts **work** demand and crew
capacity. Nothing forecasts **network** demand or plans the network — and network planning
is where most capital work originates. The model begins at `1.1 Capture work demand` with
the demand already existing.

### 3. 10.2.1 Manage capital program for productive assets (19209)

Define the capital investment plan (19210), monitor the capital programme (19211), secure
construction financing (19212).

The model has `2.4.1 Validate funding and budget availability` at the individual work
item, and nothing above it. Programme-level capital planning is the layer that *produces*
the budget 2.4.1 checks against. ISO 55001:2024 cl. 6.2.2 requires asset management
planning at exactly this level, so this gap is visible from the standards side too.

### 4. 10.2.6 Commission new assets (11280)

Schedule commissioning (19235), **co-ordinate energization with network operations**
(19236), capture commissioning records (19237).

Nothing in the model commissions an asset. `6.3 Programme and commission endpoints`
commissions a metering endpoint and nothing else. A new main or feeder goes from
`4.2 Execute work in the field` straight to `5.1 Verify and close work` with no
energisation step — and energisation is the moment the asset becomes live plant, with its
own coordination, its own records and its own safety sequence.

### 5. 10.4.5 Perform waste and hazardous goods management (16970)

Nothing in the model handles spoil, contaminated soil, PCB-containing equipment,
transformer oil, or asbestos-containing pipe wrap. `7.4.4 Dispose of debris and restore
site` disposes of vegetation debris, and that is the whole of it. For gas and electric
distribution this is a permitted, manifested, regulated activity.

### 6. 10.4.2 Decommission productive assets (19258)

The model retires the **record** (`12.1.6 Retire and dispose of assets`) and the
**accounting** (`5.3 Capitalise and unitise completed work`) but never does the physical
decommissioning work.

### 7. 14.1.4 Monitor network status (19278)

Monitor current switch and valve state (19279), maintain historical network state data
(19280), monitor alerts and alarms (19281). The model's `1.1.2` captures a device
condition **as work demand**; it does not monitor the network. Arguably a SCADA/ADMS
boundary and defensible as out of scope — but it is currently absent by omission rather
than by decision, which is not the same thing.

### 8. 14.1.2 Develop network operational plans (11266)

Includes **19270 Create switching and network reconfiguration plans** — the planning half
of gap 1.

## Where the model puts something in the wrong place

**10.4.4 Perform abandonment (10954)** maps to `8.6.6 Purge, seal and abandon facilities`,
which sits inside **8.6 Manage gas pressure and odorization**. Abandonment is a lifecycle
end state, not a pressure-management task, and 49 CFR 192.727 governs it in its own right.
The mapping is right; the home is wrong.

## Where the model is better than APQC, and should stay that way

APQC compresses into `10.3.1 Plan asset maintenance` (seven activities) what this model
spreads across six groups: 1.3 categorise and prioritise, 1.4 generate programmed work,
2.5 package work, 3.1 forecast, 12.4 assess condition, 12.5 define maintenance strategy.
For a *work management* reference that granularity is correct and APQC's is too coarse —
APQC is a benchmarking taxonomy, not a process model. The same holds for `10.3.2 Manage
asset maintenance`, which flattens scheduling, resourcing, quality, records, safety and
performance measurement into one process.

**This is the reason APQC is structural precedent and not an authority.** Where APQC is
coarser, the model wins. Where APQC has a process the model does not have at all, APQC is
evidence of an omission — and that is what the eight above are.

## What is not concluded here

No model change has been made. Eight absences and one misplacement are a finding, not a
decision. Three of the eight (capital programme, network planning, network status
monitoring) may be legitimate scope boundaries for a work-and-asset-management model
rather than gaps — but if so they should be *recorded as scope decisions* in the model,
which they currently are not. Two of them (planned network operation, commissioning) look
like genuine omissions that a utility would notice immediately.

This bears directly on the open question in
`research/Reference Derivation - Standing Issue.md`: the taxonomy above the specification
layer is itself two-programme derived and has never been tested. It has now been tested
against one of the two frameworks that recommendation named. It did not come through
clean.


## The other direction, and the one that sells the reference

Both crosswalks were authored framework-to-model: for every APQC process and every GFMAM
subject, where does it live here. That direction answers "have we missed anything they
have". It cannot answer the question a buyer actually asks, which is what this reference
carries that the free frameworks do not name at all.

Computing it from the same rows — a category is reached when any crosswalk row names it —
gives this:

| | reaches | absent |
|---|---|---|
| APQC PCF Utilities, categories 10 and 14 | 15 of 19 | 7.0, 11.0, 14.0, 16.0 |
| GFMAM Asset Management Landscape 3rd ed. | 18 of 19 | 11.0 |

Two of APQC's four absences are artefacts of scope rather than real gaps, and saying so is
the honest reading. **14.0 Manage Workforce and Time** and **16.0 Manage Contractors and
Partners** both have counterparts in APQC's *cross-industry* categories — 7 Develop and
Manage Human Capital, and 4.2.4 Manage suppliers. The extraction here covers categories 10
and 14 only, because those are the two that carry utility content, and cross-industry
manufacturing supply chain is not field-crew contracting. So the finding for these two is
narrower than "absent": APQC has nothing *utility-specific* to say about either.

The other two are real.

**7.0 Manage Vegetation** has no APQC process at any level. It is the single largest
recurring distribution maintenance programme in the United States by spend, it is the
subject of state commission rules with mandatory cycles, and the framework does not name
it. GFMAM reaches it only through the general 6.5 Maintenance Delivery.

**11.0 Manage Joint Use and Third-Party Attachments** is absent from *both* frameworks.
It is not a small domain: pole attachment rates and access are governed by 47 U.S.C. 224
and the FCC rules under it, the physical arrangement by NESC Rules 235 and 238, and the
work itself — inventories, make-ready, unauthorised-attachment audits, transfer chases —
is real programme work that utilities staff and litigate over. Neither APQC nor the GFMAM
Landscape has a home for it.

That is the argument for this reference existing, and it should be made in exactly these
terms: not that the frameworks are wrong, but that they are organised on an asset axis for
an audience that is not doing the work, and two whole domains of utility work fall through
the gap. The reverse section is written into both crosswalk JSON files by their
generators, so the claim stays computed rather than asserted.

## Licence — this matters for a commercial deliverable

The Utilities PCF is **jointly developed by APQC and IBM**, and its licence is more
permissive than most standards but is conditional:

> ©2025 APQC and IBM reserve all rights in this work except as expressly granted herein.
> APQC and IBM hereby grant you a perpetual, worldwide, royalty-free license to use, copy,
> publish, modify, and create derivative works of the PCF, provided that all copies of the
> PCF include this notice, and any derivative works contain the following attribution:
>
> > This work is based in part on an Industry Process Classification Framework ("PCF"), an
> > open standard developed by APQC and IBM to promote benchmarking and best practices
> > worldwide. […] To download the full PCF […] please visit www.apqc.org/pcf.

So `apqc_pcf_utilities.json` and `apqc_crosswalk.json` may be published — they carry the
notice and the attribution in `_copyright` and `_attribution`, written by their generators
so the notice cannot drift away from the data. **Any deck, workbook or document that shows
APQC element numbers or names must carry the attribution too.** This is not a formality:
the licence grant is conditional on it, and the deliverable is commercial.

Note the contrast with the other supplied evidence. `Tim Evidence/` is gitignored because
EN 17007 and ISO 55001 are licensed standards that may not be redistributed — they are
cited by clause. APQC is the opposite case: redistribution is expressly permitted, and the
obligation is attribution rather than abstention.

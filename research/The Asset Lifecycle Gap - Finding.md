# The asset lifecycle gap

**Date** 2026-08-29 · **Platform** Claude · **Status** RESOLVED 2026-08-29 — the Asset Lifecycle band was added

## The question

Does this reference need an asset dimension, or is work management enough?

## The answer

It needs one. The model is a **work management reference with an asset information annex**.
It is not an asset lifecycle reference, and two independent authorities say the same
things are missing.

## Two frameworks, tested separately, agreeing

`build/eam/apqc_crosswalk.json` tests the model against **APQC PCF Utilities v7.2.1** —
a benchmarking taxonomy, no asset management authority. 38 level-3 processes in the two
utility categories: 12 covered, 6 partial, 8 absent.

`build/eam/gfmam_crosswalk.json` tests it against the **GFMAM Asset Management Landscape,
third edition, June 2024** — 7 subject groups, 40 subjects, and this one *is* an
authority. It is what the IAM Anatomy v4 defers to for the subjects of the discipline, and
it is free. 40 subjects: 12 covered, 13 partial, **6 absent**, 9 deliberately out of scope
(policy, leadership, culture, organisational change — management-system subjects that sit
above a process reference).

The two were authored independently, from different documents, on different axes. **Six
themes come up absent in both.** This repository's own promotion rule is *two independent
organisations plus a standards basis*. All six clear the first two legs, and ISO 55001:2024
cl. 8.1 — which requires life cycle management explicitly — is the third.

| Theme | APQC | GFMAM | Standards basis |
|---|---|---|---|
| **Planned outage, shutdown and switching** | 14.1.6 Perform planned network operation; 14.1.2 create switching plans | **3.8 Shutdown and Outage Strategy and Planning** | 29 CFR 1910.269(m) and (d) |
| **Asset operation** | 14.1.4 Monitor network status; 14.1.2 | **6.4 Asset Operation** | — |
| **Asset creation, commissioning, energisation** | 10.2.6 Commission new assets; 10.1 | **6.2 Asset Creation & Acquisition** | ISO 55001 cl. 8.1 |
| **Asset demand analysis and network planning** | 10.2.2 Perform utility network planning | **3.2 Demand Analysis**; 3.4 Planning | ISO 55001 cl. 6.2.2 |
| **Capital programme and whole-life value** | 10.2.1 Manage capital program | 3.4 Planning; **3.6 Life cycle Value Realization** | ISO 55001 cl. 8.1 |
| **Decommissioning, disposal, waste** | 10.4.2; 10.4.5 waste and hazardous goods | **6.7 Asset Repurposing or Disposal**; 3.3 Sustainable Development | 49 CFR 192.727 |

GFMAM's definition of 3.8, read verbatim from the published PDF, is worth quoting because
it names the whole gap in one sentence:

> An organisation's processes for the identification, planning, scheduling, execution, and
> control of work related to shutdowns, turnarounds, or outages (STOs).

The model does none of the five verbs in that sentence for a **planned** outage. It
consumes the result at `2.6.3 Validate prerequisites before release` and `4.4.4 Confirm
isolation and permit-to-work`, and it performs switching only during **restoration** at
`9.3.2`. A regulated, lead-time-bearing process is currently sitting in a specification
field labelled "input".

## Why the model came out this way

The four lifecycle stages APQC uses — acquire, construct, maintain, dispose — are an
**asset** axis. This model is organised on a **work** axis: identify demand, plan,
schedule, execute, close. The two are not alternatives; the work axis is what happens
*inside* the maintain stage.

Measured against the asset axis, the model covers:

| Asset lifecycle stage | Coverage |
|---|---|
| Plan and acquire | **absent** — nothing plans the network or the capital programme |
| Design and construct | **partial** — 2.1 designs and 4.2 builds, but only once a demand exists, and nothing commissions or energises |
| Operate | **absent** — 9.0 handles the unplanned case only |
| Maintain | **complete** — this is the entire model, and it is better than either framework here |
| Dispose | **records only** — 12.1.6 retires the record, 5.3 retires the accounting, nothing retires the plant |

Category 12.0 *Manage Assets and Asset Information* looks like the asset dimension but is
not. Read its six groups: register, spatial integration, linear referencing, condition
assessment, maintenance strategy, obligation register. Every one is about **knowing about
assets** or **deciding what work to do to them**. That is an asset *information* function
serving the work axis. It is good, and it is not a lifecycle.

## Where the model beats both frameworks

APQC compresses into `10.3.1 Plan asset maintenance` — one process, seven activities —
what this model spreads across six groups. GFMAM compresses the same territory into one
subject, `6.5 Maintenance Delivery`. For a work management reference that granularity is
correct and theirs is too coarse.

**This is the reason neither framework is an authority over the model's shape.** They are
evidence of **omission** when they carry something the model lacks entirely. They are not
licence to flatten a distinction the model makes deliberately.

## Resolution, 2026-08-29

The user's decision was to include the asset lifecycle. Three categories were **appended**
as a fourth band, so that nothing renumbers — categories 1.0 to 16.0 keep their ids, uids
and legacy_ids, and the specification campaign in flight is unaffected.

| New category | Groups | Processes | Closes |
|---|---|---|---|
| **17.0 Plan the Network and Capital Programme** | 5 | 26 | APQC 10.2.1, 10.2.2 · GFMAM 3.2, 3.4, 3.6 |
| **18.0 Operate the Network for Planned Work** | 5 | 25 | APQC 14.1.6 in full, 14.1.2 in part · GFMAM 3.8, 6.4 in part |
| **19.0 Commission, Decommission and Dispose of Assets** | 4 | 21 | APQC 10.2.6, 10.4.2, 10.4.3, 10.4.4, 10.4.5 · GFMAM 6.2, 6.7, 3.3 in part |

The model went from 16 categories, 89 groups and 434 processes to **19, 103 and 506**.
Every category now carries a `lifecycle` field naming the asset lifecycle stage it serves,
so the model answers ISO 55001:2024 cl. 8.1 on the asset axis while keeping the work axis
that makes it a process model rather than a benchmarking taxonomy.

**18.0 is work-facing only, by decision.** It covers the network operations that gate work
already in this model — switching plans, outage approval, notification, switching
execution, clearance issue, return to service. Real-time monitoring, alarm handling,
optimisation and protection settings are SCADA, ADMS and DERMS functions and are out of
scope. That is now recorded as a decision in the category summary and in the crosswalk,
where APQC 14.1.4 moved from `absent` to `scope` with the reason attached.

**Both crosswalks now show zero absences.** APQC: 20 covered, 6 partial, 0 absent, 12
scope. GFMAM: 18 covered, 13 partial, 0 absent, 9 scope. Everything not covered is either
partial with the remainder named, or out of scope with the reason recorded — which was the
real point. An absence a reader can see and understand is not a gap.

**The immediate payoff in the specification layer.** `2.6.3 Validate prerequisites before
release` previously took "isolation and clearance arrangement" as an input from network
operations with no producing process anywhere in the model. It now cites **18.4.4 Issue the
clearance or permit-to-work**, against a switching plan approved at 18.2.2, under 29 CFR
1910.269(m). The same correction applies to `4.4.4 Confirm isolation and permit-to-work`
when category 4.0 is specified. A clearance and a permit are different instruments and the
model now distinguishes them.

**What was deliberately not done.** 8.6.6 *Purge, seal and abandon facilities* stayed in
8.6 rather than moving to 19.2. Purging under 49 CFR 192.629 is a gas pressure operation;
abandonment under 192.727 is a lifecycle transition. The two are hooked, not merged.

## What was not concluded before the decision

No model change has been made, and none should be made mid-campaign. Three questions are
the user's:

1. **Is the asset lifecycle in scope at all?** A defensible answer is no — this is a work
   and asset *management* reference, and network planning, capital programme management
   and real-time operations belong to other systems. But if that is the answer, it has to
   be **recorded as a scope decision**, because at present these are absent by omission,
   and a client will read omission as oversight.
2. **If it is in scope, does it become new categories or a second axis?** New categories
   renumber everything again. A second axis — mapping each existing category to the
   lifecycle stage it serves — costs nothing structural and answers the ISO 55001 cl. 8.1
   question without moving a single process.
3. **The two that are hard to defend as out of scope** are planned outage and switching,
   and commissioning and energisation. Both are field work, both gate other work in this
   model, both are regulated, and a utility reviewer will notice their absence in the first
   hour.

This is the second framework test the standing issue in
`research/Reference Derivation - Standing Issue.md` recommended. The taxonomy has now been
read against EN 17007, APQC PCF Utilities and the GFMAM Landscape. It did not come through
any of the three clean, and the three disagree with it in the same places.

## Two corrections worth recording

**EN 17007 is not ISO/IEC 17007.** `EN 17007:2017 Maintenance — Maintenance process and
associated indicators` is CEN/TC 319, published 2017-11-30, and adopted nationally as
DIN EN 17007:2017, BS EN 17007:2017 and SIST EN 17007:2018. `ISO/IEC 17007` is
*Conformity assessment — Guidance for drafting normative documents suitable for use for
conformity assessment*, 2009, revised 2026. Different committees, different subjects,
coincidentally similar numbers. The confusion is easy to fall into because the supplied
copy in `Tim Evidence/` is **misnamed** `iso-170072017.docx` by whoever posted it. The
model's process spine is the maintenance standard, not the conformity-assessment one.

**The "39 subjects" figure is the Landscape's second edition.** The third edition (June
2024) has 40 across 7 groups. The IAM *Anatomy* v4 (2024-07-01) moved to a ten-box
capability model and defers to the Landscape for subjects, and there is no North
America–specific Anatomy. Cite GFMAM for subjects; cite the Anatomy only as corroboration.

## Sources

- GFMAM, *The Asset Management Landscape*, third edition, June 2024, ISBN 978-1-7774676-8-5 — https://gfmam.org/sites/default/files/2024-06/GFMAM_AM_Landscape_v3.0_English_2024.pdf
- IAM, *Release of Version 4 of the IAM Asset Management Anatomy* — https://theiam.org/news/release-of-version-4-of-the-iam-asset-management-anatomy/
- ANSI/ASTM/ISO 55001-2024, *Asset management — Asset management system — Requirements* — https://store.astm.org/ansi_astm_iso55001-2024.html
- DIN EN 17007:2017, *Maintenance process and associated indicators* — https://webstore.ansi.org/standards/din/dinen170072017
- ISO/IEC 17007:2009 / :2026, *Conformity assessment — Guidance for drafting normative documents* — https://www.iso.org/standard/42635.html
- EPRI, *Power Delivery Asset Management Decision Making Process*, 1016834, December 2008 — https://www.epri.com/research/products/000000000001016834

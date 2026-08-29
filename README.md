# Utility Work and Asset Management — Industry Process Reference

A **product-neutral, standards-derived process reference** for work and asset management at
US gas and electric distribution utilities.

**19 categories · 103 process groups · 506 processes**, organised on two axes: a work
lifecycle (identify demand → plan → schedule → execute → close) and an asset lifecycle
(plan and acquire → design and construct → operate → maintain → dispose).

## The rule that governs everything

Content enters this reference **only if a standard, a regulation or a recognised industry
body says it.** Not because it is good practice, not because a product does it, not
because it is obviously true. Where something cannot be sourced, the reference says so
in a `gaps` field, in plain words.

Every citation carries a verification status, and a status is never upgraded:

| Status | Means |
|---|---|
| `verified` | Read verbatim from the official text |
| `regulation` | Verbatim from eCFR |
| `clause-verified` | Clause number and title confirmed; the body is paywalled and its content is **not** paraphrased |
| `consensus` | An industry body, not law |
| `judgment` | Inference, attributed to nobody |

Observed practice from any individual operator is **never** merged into this reference. It
belongs in a separate specialization overlay keyed on the permanent element id (`uid`).
Promotion into the reference requires two independent organisations plus a standards basis.

## What is here

```
model/     model.json           19 categories, 103 groups, 506 processes, permanent uids
           vocabulary.json      the shared contract: IEC 61968-6 components, CIM classes,
                                the full EN 17007 catalogue, decision variables, banned
                                terms, the content budget
           apqc_crosswalk.json  this model against APQC PCF Utilities v7.2.1
           gfmam_crosswalk.json this model against the GFMAM Asset Management Landscape 3rd ed.

specs/     SCHEMA.md            the specification field set and the notation selection rule
           cat-01-*.json        category 1.0 specified — the worked example
           cat-02-*.json        category 2.0 specified

campaign/  SPEC_CAMPAIGN_PROMPT.md   the standing brief for the specification campaign
           ROUND_KICKOFF.md          the covering message and per-round values
           assignments/              a small per-category pack for each platform

research/  the decision records and the framework reads behind the model's shape
```

## The four modelling layers

1. **Specification** — the field set is EN 17007:2017 cl. 5.2, corroborated by
   ISO 9001:2015 cl. 4.4.1 a)–h).
2. **Behaviour** — BPMN 2.0, DMN 1.3 or CMMN 1.1, chosen per process. BPMN where the happy
   path can be drawn; DMN where the output is a value rather than a state change; CMMN
   where two competent people would legitimately sequence it differently; specification
   only where there is no instance boundary.
3. **Data** — the IEC 61968-11 CIM `Work` package.
4. **Landscape** — IEC 61968-6 cl. 4.2 reference components with an ArchiMate 3.2
   serving/access pattern.

`research/Process Modelling Notation - Decision Record.md` has the reasoning.

## The specification campaign

Three AI platforms specify one category each per round against an identical brief, so the
results are comparable rather than merely parallel. `campaign/` carries the brief, the
kickoff message and the per-category assignment packs. Submissions are gated by a
validator; one that does not pass is not merged.

## What is deliberately not here

- **Licensed standards.** EN 17007, ISO 55001, EN 13460 and the rest are cited by clause
  and are not redistributed.
- **Client material.** This reference is derived from published authorities. No operator's
  programme documentation, process designs or configuration appears in it.
- **Vendor content.** No product is named except where a public integration behaviour is
  the subject, and no vendor expression is ever written into a reference model file.

## Attribution

The crosswalks are derivative works of the APQC Process Classification Framework and carry
the required notice and attribution in their `_copyright` and `_attribution` fields:

> This work is based in part on an Industry Process Classification Framework ("PCF"), an
> open standard developed by APQC and IBM to promote benchmarking and best practices
> worldwide. The PCF is intended to facilitate organizational improvement through process
> management and benchmarking, regardless of industry, size, or geography. To download the
> full PCF or other industry-specific versions of the PCF, as well as associated measures
> and benchmarking, please visit www.apqc.org/pcf.

**Anything reusing APQC element numbers or names must carry that attribution.**

The GFMAM Asset Management Landscape (third edition, June 2024,
ISBN 978-1-7774676-8-5) is cited by subject number and name; subject definitions are quoted
only where read verbatim and are attributed inline.

## Status and licence

Work in progress. Two of nineteen categories are specified to tier 3; the rest carry names,
permanent ids and provenance grades but not yet their specifications.

No open-source licence is granted. © Tim Bartmann. Published for reference and review;
contact the author about reuse.

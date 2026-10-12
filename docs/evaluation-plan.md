# TechFinder — evaluation and acceptance plan

**Status:** Proposed tests and targets. No experiments have been run and no results are claimed.

[Repository](https://github.com/zainahmadlums/techfinder) · [Architecture](technical-architecture.md)

## What the prototype must establish

1. Collected fields accurately reflect their sources.
2. Listings are not merged merely because their names look alike.
3. Recommendations respect essential requirements and expose unsupported comparisons.
4. Users can tell when a price was observed and inspect the original offer.

## Planned evidence set

- **Catalogue target:** 50–100 listings from three accessible sources. Report the achieved listing count, canonical configuration count and source count separately.
- **Extraction sample:** manually audit at least 30 listings, aiming for 10 per source if three sources are available. Include both complete and incomplete specifications.
- **Matching set:** prepare 60 labelled candidate pairs: 20 identical configurations, 20 similar-name configuration conflicts, 10 unrelated pairs and 10 pairs with insufficient evidence.
- **Development versus holdout:** aim for 30 pairs each, retaining examples of every class in both sets. Keep listings and product families disjoint across the two subsets to reduce leakage. Expand the source pool or report a smaller achieved set if necessary; do not quietly reuse development products in the holdout.
- **Ground truth:** record the source evidence and a short explanation for each label before scoring predictions. Manually review ambiguous labels; record whether a second reviewer was available.

These are small prototype samples, not evidence of market-wide reliability. Publish actual counts and the limitations of manual labelling.

## Metrics and proposed targets

| Area | Measurement | Proposed acceptance target |
|---|---|---|
| Extraction | Correct normalized field values / audited fields; score each field separately and also report a pooled total | At least 95% pooled accuracy; disclose per-field errors rather than hiding them in the average. |
| Missing information | Correctly preserved unknowns / audited absent fields | 100% on the audited sample; never invent required specifications. |
| Match precision | Correct automatic merges / all automatic merges on labelled, evaluable pairs | At least 95%; report numerator and denominator. |
| Match recall | Correct automatic merges / labelled identical pairs | Report the observed value and the precision/coverage trade-off; no initial minimum. |
| Review coverage | Pairs held for review / all evaluated pairs | Report by ground-truth class so abstention is visible. |
| Conflict protection | Configuration-conflict fixtures incorrectly auto-merged | Zero on the curated critical-conflict tests. |
| Hard constraints | Eligible recommendations violating a known budget or required specification | Zero across at least 10 scenarios. Unknown required fields must not pass eligibility. |
| Provenance | Displayed prices with a source URL and observation timestamp / all displayed prices | 100% in the demonstration dataset. |
| Stale-data handling | Correct stale labels and preserved timestamps after a failed refresh | Pass both boundary and failed-refresh scenarios. |

A zero automatic-merge denominator makes precision **undefined**, not 100%. Count automatic merges on insufficient-evidence pairs separately as unsupported merges and require zero in those fixtures. Passing an aggregate precision target does not excuse a failure of a critical-conflict test.

At this sample size, report exact counts alongside percentages. Do not present a high percentage based on a handful of matches as a production guarantee.

## Critical acceptance cases

| Case | Input or trigger | Expected behavior |
|---|---|---|
| Same configuration, different title | Consistent identifiers and all critical specifications | Group offers and retain both sources. |
| RAM mismatch | 8 GB versus 16 GB | Separate configurations, even when names look identical. |
| Storage mismatch | 512 GB versus 1 TB | Separate configurations. |
| GPU or display mismatch | Same family name, different GPU or panel | Separate configurations. |
| Missing configuration evidence | RAM or exact identity unresolved | Hold for review; do not silently complete missing fields. |
| Offer terms differ | Same hardware, different condition or warranty | Keep terms visible and prevent misleading equivalent-offer presentation. |
| Budget boundary | Price equal to and then above the budget | Include at the stated limit; exclude above it. State whether delivery is known. |
| Missing required specification | Recommendation candidate has unknown required RAM | Mark unresolved; do not treat it as eligible. |
| Preference change | Two eligible, sufficiently evidenced candidates | Recompute deterministically; explain the actual criteria used. A rank change is not mandatory. |
| Refresh failure | Last successful observation is older than 24 hours | Preserve the observation time and show stale status. |
| Freshness boundary | Observation ages of 23:59, 24:00 and 24:01 | Apply the documented rule consistently: stale only when older than 24 hours. |
| Unsupported technical claim | No source for battery endurance or GPU power | Show unknown; do not present a fabricated score or factual explanation. |

## Does AI improve the pipeline?

Compare a deterministic extraction/matching baseline with the AI-assisted version on the **same holdout**. Report precision, recall, abstention, unsupported merges and errors for both, plus observed latency and model usage. Keep hard validation rules constant when isolating the effect of AI candidate retrieval or parsing.

If AI increases false merges or adds little measurable value, keep the simpler baseline for that step. Record this as a finding rather than assuming AI is automatically better.

## Small usability check

If time permits, ask 3–5 volunteers to identify the cheapest comparable configuration, explain why a cheaper variant is excluded, and locate the source/update time. Record completion, confusion and approximate time. Obtain their consent and report only anonymous summaries. This convenience sample is exploratory; it cannot establish population-wide time savings.

## Results report template — complete after testing

| Item | Result |
|---|---|
| Dataset capture dates and source access method | Not measured |
| Retailers / listings / configurations | Not measured |
| Development and holdout pair counts | Not measured |
| Extraction accuracy by field | Not measured |
| Automatic-merge precision and recall, with counts | Not measured |
| Review rate and unsupported merges | Not measured |
| Baseline versus AI-assisted comparison | Not measured |
| Critical acceptance cases passed / attempted | Not measured |
| Recommendation constraint violations | Not measured |
| Provenance coverage and stale-data tests | Not measured |
| Optional usability observations | Not conducted |
| Known failures and next fixes | To be documented after testing |

Include failures, excluded sources, manual interventions and curated-data use in the final report. Retain the labelled cases so the demonstration can be reproduced.

# TechFinder — demo storyboard

**Design artifact, not an implemented feature report.** All examples below are synthetic. Prices are illustrative PKR values, not shopping advice or current offers.

[Repository](https://github.com/zainahmadlums/techfinder) · [Proposal](../proposal.md) · [Interface concept](../assets/techfinder-concept.svg)

## The buyer and the decision

A university student needs a laptop for programming and occasional gaming, has a PKR 250,000 budget, and requires at least 16 GB RAM and 512 GB storage. These are example requirements for the demonstration, not findings from user research.

The central moment: a PKR 215,000 listing looks cheaper than a PKR 239,000 listing, but it has only 8 GB RAM. TechFinder should make that difference obvious before the buyer follows a purchase link.

## Synthetic demonstration data

The product identifiers and retailer names below are invented. In the example, source evidence explicitly supplies each listed specification.

| Listing | Retailer | Configuration ID | RAM / SSD | GPU | Price | Expected treatment |
|---|---|---|---|---|---|---|
| A1 | Retailer A | TF-16-512 | 16 GB / 512 GB | RTX 4050 | PKR 239,000 | Group with A2 after all critical specifications are checked. |
| A2 | Retailer B | TF-16-512 | 16 GB / 512 GB | RTX 4050 | PKR 249,000 | Same synthetic configuration as A1. |
| A3 | Retailer C | TF-8-512 | 8 GB / 512 GB | RTX 4050 | PKR 215,000 | Separate configuration; fails the example RAM requirement. |
| A4 | Retailer D | Not supplied | Unspecified / 512 GB | RTX 4050 | PKR 229,000 | Hold for review; do not infer RAM or model identity. |

For the A1/A2 grouping fixture, CPU, display, regional variant and condition must also be supplied and consistent. The abbreviated table is not sufficient evidence by itself. A matching test will use the complete source records.

## Screen 1 — describe the need

**Inputs:** budget, workload, minimum RAM and storage, plus adjustable preferences such as performance, portability and display quality.

**Visible response:** an explanation of which inputs are hard requirements and which affect ranking. A device that fails a hard requirement must not become eligible because it has a good weighted score.

**Acceptance:** every displayed recommendation satisfies the known hard requirements. Unknown required specifications remain unresolved rather than being assumed to pass.

## Screen 2 — compare a suitable configuration

Show the TF-16-512 product with its specifications and two offers: PKR 239,000 and PKR 249,000. Show source links, update times and any differences in warranty, condition or delivery charges.

In this fixture both offers are new, have the same stated warranty, and exclude delivery. The price difference is PKR 10,000 **between these two example offers**, not a claim about market-wide savings or total checkout cost.

**Acceptance:** the two retailer listings are grouped only when identity and critical configuration checks pass. A buyer can inspect the reason for the match.

## Screen 3 — expose the misleading comparison

Display A3 separately with the explanation:

> Different configuration: 8 GB RAM. Your requirement is at least 16 GB. This offer is excluded from the exact-configuration comparison.

Display A4 as unresolved:

> RAM and configuration identity are missing. More evidence is needed before comparing this as an identical product.

**Acceptance:** neither listing can silently become the lowest-price offer for TF-16-512. Possible upgrades are not treated as already installed, and their cost is not invented.

## Screen 4 — explain recommendations and uncertainty

Once another eligible product has enough evidence for comparison, change the performance/portability preferences and show the resulting explanation. Use measured or sourced attributes for scoring; do not invent battery endurance or GPU power limits.

A rank change is expected only if the candidate evidence and weighting justify it. If missing data prevents a sound comparison, show that limitation instead of manufacturing a definitive winner.

**Acceptance:** ranking is reproducible for the same inputs, satisfies hard constraints, and links factual claims to the underlying evidence.

## A 90-second presentation script

| Time | Demonstration | Point to communicate |
|---|---|---|
| 0–15 sec | Introduce the student's budget and requirements. | Buyers need help deciding what is suitable, not merely what is cheapest. |
| 15–35 sec | Open the two comparable TF-16-512 offers. | Different retailer titles can describe the same configuration. |
| 35–55 sec | Reveal the cheaper 8 GB variant and the unresolved listing. | Incorrect merging makes a price comparison misleading. |
| 55–75 sec | Inspect evidence and change recommendation preferences. | Recommendations should expose their reasoning and uncertainty. |
| 75–90 sec | Show measured results, source coverage and limitations. | Reliability is testable; remaining gaps are explicit. |

Until a prototype exists, present this as a **planned demonstration** and use the static concept. Replace planned claims with observed behavior only after testing.

## Before the final presentation

- Use dated data and label any curated snapshots.
- Prepare one verified match, one conflicting configuration and one incomplete listing.
- Confirm purchase links and the displayed freshness labels.
- Report both successful integrations and unavailable sources.
- Present measured results with sample counts, including failures.
- Keep the static concept as a clearly labelled backup, not as evidence of a working app.

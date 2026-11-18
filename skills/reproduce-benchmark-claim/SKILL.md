---
name: reproduce-benchmark-claim
description: Check whether a performance or accuracy claim follows from the original inputs, metric and shipped configuration. Use before quoting a number or comparing runs, not to choose a model from published rankings.
license: MIT
---

# Reproduce a benchmark claim

Start with the exact sentence someone wants to publish. Identify the population, measured operation, unit, baseline, and shipment or experiment it describes.

- Freeze the inputs before running either version: record their IDs or manifest digest, the split, preprocessing, metric version, model and settings. For timings, also record hardware, warm-up, cache state and background load. If the old inputs cannot be recovered, label the new run as a new baseline, not a reproduction.
- Run both versions through the same entry point on the same cases. If the claim is about the app, use the app's settings, not a raw model. Record missing results, failures and timeouts by case ID. Report timeout counts separately; the cutoff is not an observed completion time. Never silently score only the intersection of successful runs.
- Recompute from per-case observations. Define the denominator. For corpus word error rate, divide total substitutions, deletions and insertions by the total reference words. Do not average per-clip percentages. For latency, state the percentile or median, the measured interval, repetitions, and whether loading is included.
- Check whether differences exceed ordinary variation. Preserve both wins and regressions. Distinguish measured zero from a missing measurement. Quoting a third party's result requires that their population and metric match the sentence.

Return the narrowest supported sentence with its method, sample count and evidence location. If the comparison isn't valid, name the mismatch and the smallest rerun that would settle it. Do not upload private inputs as evidence.

Example: two clips have 1 error in 2 reference words and 1 in 18. Corpus word error rate is 2/20, or 10%, not the mean of 50% and 5.6%. If a third clip is missing, the 10% describes those two clips only.

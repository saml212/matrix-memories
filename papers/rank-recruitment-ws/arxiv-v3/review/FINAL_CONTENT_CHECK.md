# Final content check — When the Gradient Sees Rank

Date: September 11, 2026.

**Verdict: PASS for the focused final content check. No remaining publication blocker was found within this review's scope.** The necessary scientific wording and release-reference corrections are applied. No new experiments, numerical changes, or broad rewrite are required.

## Scope and reviewed version

This review checked the final corrections against the earlier read-only findings, verified headline results against the existing evidence, and checked public availability of the supporting code and selected raw archives. It is not a new comprehensive scientific or novelty review, detector run, or render inspection. The source review is final; the final PDF render review is separately pending. Submission processing is handled separately.

Reviewed source: `/Users/samuellarson/experiments/paper-reading/rankrecruit-submission-2026-09-11/source`.

Canonical evidence repository on the Mac mini: `/Users/samuellarson/Experiments/learned-representations`, inspected over SSH. The original current-v2 review used commit `a29c21c04f1ce9a98f13005e464fd5264877b905`.

Snapshot SHA-256 values after the corrections:

| File | SHA-256 |
|---|---|
| `source/main.tex` | `b7c9b55c447366f85ccafb394873954644df62cbc0399491ef9f1a0f5034717d` |
| `source/refs.bib` | `3afc7c9f1597d3938e42c161f4eeb035cadb811fe67eb0bdab227d5cf9059462` |
| `source/main.pdf` | `ffd74c3ebf2dc6860e855da406f3762b3478df51cfe358dbc00a1436001792b8` |

## Corrections verified

- `source/main.tex:52–54`: the title now says “Composition,” removing the unsupported implication of empirically exact vector equality. The abstract and setup retain the explicit distinction between cosine greater than 0.9 and mathematical equality.
- `source/main.tex:68`: the author's approved phrase “In our earlier study” is preserved exactly.
- `source/main.tex:88–90`, `source/sections/04_composition.tex:30–31,46–47`, and `source/sections/07_limitations.tex:34–35`: the predicted cosine curve is correctly described as using the entity-subspace operator and ideal cycle. The earlier “eigenspectrum alone” claim is removed. `source/sections/06_related.tex:31` consistently refers to predicted cosine.
- This prediction wording matches `matrix-thinking/chapter2/analyze_zdump.py:264–291,410–423`: the calculation uses powers of the full restricted learned operator and ideal cycle, with synthetic keys derived from the ideal cycle. It does not use eigenvalues alone. The retained “without raw keys” statement is accurate.
- `source/sections/07_limitations.tex:77–80`: the reproducibility paragraph includes the actual public repository URL and accurately says that per-run JSON archives support the numbers. It no longer implies released model-weight checkpoints. The dimension-sweep archive's `checkpoints` are evaluation metrics; `run_stage0.py:293–298` appends evaluation results to that field.
- `source/refs.bib:21–22`: the earlier paper now has its public identifier and link, [arXiv:2609.03090](https://arxiv.org/abs/2609.03090). `source/refs.bib:29` describes the other companion as submitted to arXiv, without claiming it has already been posted. Its submission status was confirmed by the coordinating agent from the author's account; this reviewer did not independently inspect that account.

The complete source comparison against v2 contains only these publication corrections and source-header changes. Reported results, numerical table rows, and evidence tags are unchanged. Both vector figure PDFs are byte-identical to v2.

## Headline evidence checks

Checks use the claim identifiers in [the existing brief](https://github.com/saml212/matrix-states/blob/main/papers/rank-recruitment-ws/brief.md). Public raw files were fetched without authentication; MD5s match that brief.

| Evidence | Independent check | Result |
|---|---|---|
| R1 | The ten d=16 grid values for K=1 through 16 are strictly increasing; anchors are 2.4219, 8.1984, and 15.0885 at K=1,8,16. K=3 is marginally above the registered band. | Matches monotonicity, Spearman rho=1.0, rounded anchors, and K<=3 band wording. |
| R2 | d=8, K=4 rank caps 1,2,3 give 0, 0.0004, 0; cap 4 gives 0.9675. | Matches <=0.0004 and 0.97. |
| R3 | Seeds 1–3 have recovery 1.0 at all eight evaluated depths; seed 4's minimum is 0.999633789. Seed 0 has 0.926757813, 0.161315918, and 0.000122070 at depths 1,7,21. | Matches four of five seeds >=0.9996 and the reported outlier. |
| R4 | Re-ran the existing read-only subspace analysis. Predicted cosines at depths 1,3,5,7,21 are 0.931719723, 0.925758057, 0.918096257, 0.908854440, 0.753567362. Maximum absolute error against measured cosine through depth 7 is 0.007445082. Recovery at depths 1,7,21 is 0.996032715, 0.881225586, 0.060363770. | Matches the table, the <0.008 claim, and rounded recovery values. |
| R5 | Recomputed the four converged seeds' entity-subspace decompositions: mean effective rank approximately 7.9987–7.9998; scale-corrected residual 0.7388–2.3837%; mean leakage approximately 0.44–1.46%; complement spectral radius 1.0175–2.8557. | Matches the reported ranges and approximate-subspace interpretation. |
| R6 | Public 80K archives contain three successful K=12 seeds and two successful K=16 seeds through shallow depths. K=16 seed 2 falls to 0.261749 at depth 21, consistent with the brief's scoped convergence description. | Matches the body counts; does not imply all K=16 successes remain accurate at depth 21. |
| R7 | d=32 cosine values 0.876809/0.909290/0.914464 and recovery 0.413086/0.632446/0.653320; effective ranks 7.29627/7.76210/7.67988. d=48 cosine 0.719644 and recovery 0.001953; d=64 cosine 0.388167 and recovery 0. | Matches all displayed rounded values and the 91–97% effective-rank range. |
| R9 | All inspected K=8 composition archives report `n_params=170896`. | Matches the model-size statement. |

R8's historical budget comparisons and other unchanged non-headline claims retain their existing brief and prior-review provenance; this focused pass did not re-run every historical experiment or re-audit every citation.

## Public availability verified

[saml212/matrix-states](https://github.com/saml212/matrix-states) is publicly accessible. HTTP 200 was confirmed for the training/evaluation runners `run_task_d.py` and `run_task_e.py`, `analyze_zdump.py`, `papers/rank-recruitment-ws/figures/figure_gen.py`, and the brief.

All 18 selected raw evidence files returned HTTP 200 and matching MD5s:

- The R1/R2 `AGGREGATE_latest.json` snapshot.
- The five K=8 unconstrained 40K Z-dump archives and the converged rank-7 seed-2 archive (R3–R5).
- The six K=12/K=16 seed-0/1/2 80K archives (R6).
- The three d=32 100K archives, d=48 100K archive, and d=64 150K archive (R7).

This supports the revised public-code-and-results statement. It does not claim a separately tagged GitHub release, universal checkpoint availability, or public availability of every large artifact elsewhere in the repository.

## Prior review status, accurately carried forward

- The parent `gauntlet/round-1/05_format_audit.md` records zero critical or serious findings and independent evidence recomputation. `07_final_review.md` cleared content, numbers, scoping, formatting, and render after required changes. `08_decision_record.md` records resolution of companion overlap and stale bibliography housekeeping.
- `detector/round-1.md` records one round with two independent judgments of “100% human,” no cited tells, and discharge under its explicitly documented local bounded protocol. It is **not** evidence of two consecutive rounds under the paper skill's generic detector protocol, nor proof of human authorship.
- The September 10 v2 prose recheck passed. Its six-page visual inspection reported no findings. Those reports describe the earlier build, not the newly revised v3 PDF.
- The September 11 author-approved abstract follow-up separately records a successful six-page build and page-one inspection, with PDF SHA-256 `51ead38b1d8a7c3a57e12c1c086c350e3badc4deda6a7697bc5440eb8454734d`. This was the v2 PDF independently checked during the initial submission review.
- The old workshop CFP verification and anonymized-code conditions were specific to the earlier workshop submission route. They do not apply to this named arXiv source.

No manuscript files were edited by this reviewer. This report is the only output written for the correction recheck.

# Companion paper: prose and layout revision

September 10, 2026. Working draft `arxiv-v2` of **When the Gradient Sees Rank: Provable Necessity, Causal Recruitment, and Exact Composition in Trained Matrix Memories**.

Sam requested an AI prose scrub and visual/spacing check before the teaching walkthrough. This revision addresses writing and presentation, with source checks for technical wording. It is not a new experiment, a complete scientific/novelty review, or a submission. The v1 source and PDF remain intact.

## Prose changes

- Replaced metaphor-heavy headings and phrases (“teeth,” “dead cells,” “launder rank,” “rank-starved”) with descriptions of the task, rank caps, recovery, and training budget.
- Broke compressed paragraphs into direct sentences and defined the reported metrics in captions.
- Stated the task before the motivation and separated the algebraic rank requirement from the experiment's cosine-greater-than-0.9 recovery threshold.
- Changed “one-for-one” growth to monotonic growth: Spearman rho=1.0 establishes ordering, not unit slope.
- Replaced exact empirical equality claims with their reported measurements: effective rank 7.999–8.000, nonzero residuals, and small but nonzero leakage.
- Brought the depth-21 caveat into the main composition explanation: on an 8-cycle, depth 21 repeats the depth-5 target and tests additional operator applications.
- Removed the unsupported attribution of every low-rank failure to representational limits. The existing aggregate lacks per-seed numerical-instability diagnostics; the revision states that limitation.

## Corrections checked against implementation and protocol

- **Adam, not plain SGD.** `matrix-thinking/chapter2/run_task_d.py:117` and `run_task_e.py:138` instantiate `torch.optim.Adam`.
- **Effective rank is exp(entropy), not entropy.** `rank_utils.py:42–54` normalizes singular values, computes entropy, then returns its exponential.
- **Rank cap means at most k, with gradients through projection.** `rank_utils.py:21–39` projects through the leading eigenspace without detaching; the training runners call loss.backward().
- **Composition reuses one entity-vector set.** `task_e.py:27–36` defines the one-step values as the successor keys. The revised notation states k_i=e_i, v_i=e_pi(i), prediction Z^h e_i, and target e_pi^h(i), avoiding the previous ambiguous value indexing.
- **Reference recovery is defined.** `TASK_D_PREREGISTRATION.md:181–182` defines the ceiling as the unconstrained model's converged recovery; the appendix now says this directly.
- **Larger-dimension rank measure is effective rank.** The R7 evidence row in `papers/rank-recruitment-ws/brief.md` records effective_rank_mean 7.762/7.296/7.680 against K=8, supporting the unchanged 91–97% range.

## Layout changes

- Added one body-text line between each table's bottom rule and its caption, overriding the template's assumption that table captions appear above tables.
- Kept Appendix B's heading and table together, before Appendix C. The table no longer interrupts the reproducibility paragraph.
- Displayed both original vector figures at text width rather than 92% width, and placed them after their task/results introduction.
- Set the rank inequality on its own line.
- Kept the larger-dimension recovery paragraph together across the page boundary.

## Preserved and deferred

The title, author, bibliography entries, experimental datasets, and reported numerical values are preserved. Both plotted PDF files and every numerical table row are byte-identical to v1. All original evidence identifiers remain. No training or data regeneration was performed.

The title still says “Exact Composition.” This scrub retains the title for the author's reading review; the body now explicitly distinguishes exact linear equality from the empirical threshold. Public repository/release links and final citation metadata should be checked at the later submission-preparation stage. No companion submission has been made or authorized.

## Validation

Fresh independent original-prose and original-render audits identified the issues above. A fresh prose recheck passed after the corrections. Final visual inspection and source-preservation checks are recorded in the accompanying review files. The build uses Tectonic on the Mac mini, three passes with intermediates and logs retained. One underfull bibliography line is a non-fatal spacing warning; there are no overfull boxes or unresolved references.


## Author-approved abstract follow-up - September 11, 2026

Changed “A prior negative result used a” to “In our earlier study, we used a” at the author’s request. The introduction already cites the earlier paper (`larson2026gradient`); that citation remains there, and no citation was added to the abstract. arXiv permits references in abstract metadata (https://info.arxiv.org/help/prep.html#abstract-required), but this abstract does not need one. This is a wording change only; scientific claims and results are unchanged.

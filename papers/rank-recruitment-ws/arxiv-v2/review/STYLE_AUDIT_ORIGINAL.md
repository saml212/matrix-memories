# Companion v1 prose audit

Read-only audit of `original/main.tex` and `original/sections/*.tex`, 2026-09-10. Scope: prose clarity, terminology, captions, and internal consistency. Title, mathematical results, numerical values, citations, and evidence tags are to be preserved. No experiments, literature reassessment, or authorship-detection claims are recommended.

The original is already free of the styleguide's banned words. Its main problem is compressed and metaphorical prose that sometimes turns approximate measurements into exact claims. The recommendations below address those sentences, rather than broadly rewriting neutral prose.

## Mechanical style checks

- Banned whole words: **0**.
- First-person singular: **0** in prose.
- Contractions: **0**.
- Conversational em-dashes: **0**.
- Rhetorical-question headings: **0**. Several declarative headings still use an unnecessary metaphor, identified below.
- Abstract: **218 whitespace-delimited tokens** in the extracted PDF, or **215** after joining three line-wrap hyphenations. This is within the 200–230 band; expansion is not needed.
- Apparatus bragging: none. Parameter counts are relevant scope information, not bragging.
- Anonymization: not applicable to this named arXiv version.

## Exact recommendations, ordered by source

### 1. `main.tex:62–88`: abstract

The phrases “every rank-evading shortcut,” “composes exactly,” and “restricted rank exactly K” are stronger than the reported empirical evidence. The original also omits the operational cosine threshold while saying the readout is “pinned to exact continuous recovery.” Keep the title. Suggested replacement abstract below (206 whitespace-delimited tokens in plain-text form; TeX math tokenization may differ). Retain the corresponding evidence tags after their findings.

> Matrix-valued fast-weight memories can represent associations through a learned linear map. Whether gradient-based training recruits the rank required by such a map remains open: a prior rank-insensitive model was tested on a task admitting a rank-1 solution. We study tasks for which exact recovery requires $\rank(Z) \geq K$, using a fixed linear readout and a single matrix state. We score recovery by the fraction of queries with cosine similarity above 0.9, distinguishing this empirical criterion from exact equality. The readout excludes argmax decoding, under which a rank-$m$ memory can store roughly $md$ associations, and unsuccessful configurations are re-tested at 2--2.5 times the training budget. Learned effective rank tracks $K$ across the tested grid (Spearman $\rho = 1.0$ at $d = 16$). Training with rank caps produces a transition near $k = K$: at $d = 8$, $K = 4$, rank 3 gives at most 0.0004 recovery and rank 4 gives 0.97. Four of five composition seeds reach $\recninety \geq 0.9996$ through 21 self-applications. Their entity-subspace operators have effective rank 7.999--8.000 for $K = 8$. In the single converged rank-starved seed, the eigenspectrum predicts the cosine decay within 0.008 through depth 7. These results connect task-imposed rank requirements to learned memory structure and performance under rank constraints.

### 2. `sections/01_intro.tex:4–25`: motivation and contribution list

Replace “carry a structural observable a vector does not have ... destroy performance” with:

> Matrix-valued states in continuous chain-of-thought models \citep{hao2024coconut} and fast-weight architectures \citep{schlag2021linear} can be studied through their rank. For tasks with a fixed linear readout, rank can limit how many linearly independent values the state recovers.

Replace “a $d \times d$ latent bolted onto a vector-pretrained GPT-2” with “a $d \times d$ latent added to a vector-pretrained GPT-2.”

Replace the text from “its own stated confound” through the contribution list with:

> ProsQA admits a rank-1 solution, so those flat curves do not establish what happens on tasks that require higher rank. We study matrix-state models trained from scratch on tasks for which exact recovery requires $\rank(Z) \geq K$. A fixed linear readout and a single-state bottleneck enforce the assumptions of this requirement. We examine the readout and bottleneck conditions (\S\ref{sec:setup}), learned effective rank and interventions during training (\S\ref{sec:recruit}), repeated composition and its subspace structure (\S\ref{sec:compose}), and recovery at larger state dimensions and training budgets (\S\ref{sec:frontier}).

This removes the metaphors “confound,” “teeth,” and “genuine ... can pass” without changing the task or contributions.

### 3. `sections/02_setup.tex:1–30`: setup headings and decoder explanation

Change section heading to `Task, Rank Requirement, and Readout Controls`.

At lines 11–13 replace “We measure whether a trained, bottlenecked model ... causally load-bearing” with:

> We measure the effective rank learned by a model with this bottleneck, and test recovery when its matrix rank is constrained during training.

Change first control heading to `Fixed linear readout.` Keep the cited argmax construction, but replace lines 18–22 with:

> This decoding rule differs from exact vector recovery and does not impose the same rank requirement. Here the prediction is the linear readout itself, $\mathrm{pred} = Z k_j$, with no argmax or learned decoder. Our empirical metric, $\recninety$, is the fraction of queries whose prediction has cosine similarity greater than 0.9 with the target. This threshold measures approximate recovery; the rank inequality above concerns exact equality.

The claim that rank one “passes at every K we test” needs an explicit meaning of pass and may depend on the cited construction's regime. Prefer the scoped contrast above unless the evidence supporting that exact statement is available.

Change second control heading to `Single-state bottleneck.` Replace its paragraph with:

> Access to the original binding tokens would allow the decoder to retrieve values without storing all bindings in $Z$. We therefore require the decoder to depend only on $(Z,\mathrm{query})$. After the encoder writes $Z$, we corrupt the raw-input cache and verify that decoding is bit-for-bit unchanged.

If the test is specifically a gradient blank-out test, the method should say what gradient was blanked; corrupting a cache and comparing outputs is described here as a behavioral check. Do not invent a gradient test in the rewrite.

### 4. `sections/02_setup.tex:33–42`: model and effective-rank definition

Make the opening fragment a sentence:

> A Transformer encoder processes the binding tokens. Its $d$ learned row-reader latents produce the rows of $Z \in \R^{d\times d}$. The encoder is permutation-invariant and can express matrices of rank up to $d$; it does not hard-code $\sum_j v_j k_j^\top$.

The definition “Effective rank (entropy of the normalized singular-value spectrum)” appears mathematically incomplete. Standard entropy effective rank is **the exponential of entropy**, not entropy itself. Verify against the implementation, then use:

> Effective rank, the exponential of the entropy of the normalized singular values, is the pre-registered primary metric.

Optional concise formula if space permits: $\exp(-\sum_i p_i\log p_i)$, with $p_i=\sigma_i/\sum_j\sigma_j$.

Replace “constrains Z to rank k” with “constrains Z to rank at most k.” This accurately describes truncated spectral projection and avoids implying the projected result is guaranteed to have rank exactly k.

Verify “plain SGD” and the later “SGD recruits” against the optimizer configuration. If an Adam-family optimizer is used, “gradient-based training” is the safe accurate term.

### 5. `sections/03_recruitment.tex:4–11`: recruitment trend

Replace “rises one-for-one with binding count” with “increases monotonically with binding count.” Spearman correlation 1.0 supports monotonic ordering; the cited values 2.42, 8.20, and 15.09 do not establish unit slope.

Replace “leaving ... only at ... by overshoot” with “exceeding the pre-registered ... band only at ...”.

Replace “A subsequent, larger replication sweep is directionally identical” with “A larger replication sweep shows the same increasing trend.” Preserve R1b.

### 6. `sections/03_recruitment.tex:17–36`: caption and causal comparison

Suggested figure caption:

> Recovery of key--value bindings under a rank cap applied throughout training. $\recninety$ is the fraction of queries with prediction--target cosine similarity above 0.9; dashed lines mark $k=K$. The archived sweep shows a transition near this rank requirement in configurations whose unconstrained models achieve high recovery.

In the body, replace “the step is exact ... a discontinuity at the provable bound” with:

> At $d{=}8,K{=}4$, $k\leq3$ yields $\recninety\leq0.0004$, whereas $k=4$ yields 0.97. The observed recovery transition occurs at the rank required for exact linear recovery.

Replace “post-knee non-monotonicity from seed noise ... ragged ramp, not a clean step” with:

> The $d{=}16$ configurations show transitions near $k\approx K$, with some non-monotonic variation above the transition; the replication shows a more gradual transition at $K{=}12$.

“From seed noise” is a causal attribution not established by this aggregate alone.

Replace the final two-sentence conclusion with:

> These results show that gradient-based training can recruit task-relevant rank under the specified architecture and readout. The flat truncation curves reported by \citet{larson2026gradient} on a rank-1-solvable task do not rule out this behavior.

The original attributes the prior result entirely to its task despite architecture, pretraining, and readout also differing.

### 7. `sections/04_composition.tex:4–43`: composition measurements and figure caption

Replace “A single full cycle is load-bearing” with “Using a single full cycle limits repeated targets caused by short permutation cycles.” Add the already-established caveat in the same paragraph:

> Depth 21 repeats the depth-5 target because $21\bmod8=5$; it tests stability under additional applications (Appendix~\ref{app:period}).

Change paragraph heading `Exact composition.` to `Composition recovery.` The numerical paragraph otherwise needs only “has not converged at the allotted budget” instead of “is still transitioning at budget.” Do not equate the >0.9 criterion with exact equality.

Suggested figure caption:

> Recovery under repeated application of the trained matrix ($d{=}16$, $K{=}8$). \emph{Left:} measured mean cosine for the converged rank-capped $k{=}7{=}K{-}1$ seed and the prediction from its eigenspectrum. \emph{Right:} $\recninety$, the fraction of queries with cosine above 0.9, for four converged unrestricted seeds, the rank-capped seed, and the unrestricted seed that had not converged. The four converged unrestricted seeds remain at or above 0.9996 across tested depths.

At lines 35–43, replace “provably insufficient” with “insufficient for exact linear recovery,” and avoid saying a **mean** above 0.9 itself passes the per-query recovery metric. Suggested first clause:

> With a rank cap $k=K-1$, the one converged seed has mean cosine 0.92--0.93 at $h\leq5$, while its recovered fraction falls with depth...

### 8. `sections/04_composition.tex:47–63`: subspace and nonzero leakage

Replace “the whole-matrix number is the wrong instrument” with “whole-matrix effective rank therefore does not isolate the subspace used by the task.”

Keep all numerical measurements but remove the claim that a query “never leaves” the entity subspace: nonzero leakage is explicitly measured. Suggested sentence ending:

> Leakage out of $\mathcal{E}$ is below 1.5\% of the state norm. The complement block is full-rank and non-contractive, while the observed trajectories maintain high recovery through the tested depths (Table~\ref{tab:subspace}, Appendix~\ref{app:subspace}).

Replace final sentence with:

> On the task's entity subspace, effective rank is close to $K$. Unsuccessful rank-capped seeds also fail this restricted-subspace test.

This preserves the observed mechanism, while avoiding “holds exactly” and “collapse is real,” neither of which the approximate measurements establish.

### 9. `sections/05_frontier.tex:1–35`: training budget and larger dimensions

Change heading to `Training Budget and Recovery at Larger Dimensions`.

Replace “Three independent axes each declared a cell dead ... reversed the verdict” with “Longer training changed whether configurations met the convergence criterion in three sweeps.”

Replace “an 8K-budget wall ... dissolving ... onset” with “configurations at $d\geq32$ that had not converged by 8K steps improved by 20K, with onset between 6K and 16K steps.”

Replace the “cell is not dead” rule with “We therefore re-test unsuccessful configurations at 2--2.5 times the initial training budget before classifying them as training failures.”

Use “did not converge through 120K steps” for “stayed dead through 120K steps.”

Replace the second paragraph opening with:

> Longer training does not eliminate the decline in recovery at larger matrix dimensions. With $K=d/4$ and encoder width $h=64$, all reported training curves had plateaued, but mean cosine decreased as $d$ increased:

Keep every measurement. Replace “exact-match metric” with “thresholded recovery metric,” and the final sentence with:

> Effective-rank recruitment and recovery can differ: at $d{=}32$, recruited effective rank reaches 91--97\% of target while $\recninety$ remains below the pre-registered 0.7 criterion.

Confirm “recruited rank” is indeed the same effective-rank metric in the cited experiment before this local terminology change.

### 10. `sections/06_related.tex:4–38`: related work and limitations

Replace “is the nearest neighbor: a hand-built existence construction” with “construct a linear associative memory.”

Replace “this work pins the readout so that construction cannot pass” with “we instead use a fixed linear readout and assess continuous vector recovery.” Keep the citations.

Replace “the compositional-generalization caution ... is met with an exact eigenstructure match” with:

> Our composition analysis compares the learned operator with the ideal cycle on the entity subspace, providing a structural check alongside the recovery measurements \citep{dziri2023faithfate,wang2024grokked}.

The residual 0.7–2.4% does not establish exact eigenstructure equality.

Replace “not an $n>1$ mechanism” with “the spectral comparison is therefore a single-seed case study.” Retain the other two numerical failures and single-seed high-dimension limitation.

Replace “The registered falsifiers stand” with “The registered failure criteria are listed in Appendix ...”. If these are specifically counterexamples that would refute a claim, “registered counterexamples” is more precise than “failure criteria.”

Replace companion description with:

> A companion paper \citep{larson2026ranklaw} studies the relation between group dimension and effective rank in group-composition state tracking. It cites the binding measurement developed here and shares no figures or tables with this paper.

### 11. `sections/07_limitations.tex:6–19`: depth-21 appendix

Replace “so repeated self-application does not amplify their residual error” with “so the additional applications do not reduce thresholded recovery below that level.” The metric does not rule out growth in errors that remain below its threshold.

Replace “compound a passing shallow-hop cosine into collapse (0.947 ... in recovered fraction)” with:

> reduce $\recninety$ from 0.947 at $h{=}5$ to 0.060 at $h{=}21$.

This corrects a metric mix-up: 0.947 and 0.060 are fractions, not cosine values.

### 12. `sections/07_limitations.tex:35–69`: table captions

For Table 1, specify $(d,K,k)=(16,8,7)$ and define $\recninety$ in the caption. Replace its last sentence with:

> Predicted and measured mean cosine differ by less than 0.008 through $h=7$. At $h=21$, mean cosine is 0.8206 and only 0.060 of queries exceed the 0.9 threshold.

This removes “exact-match” and “moves little” while using the table's own values. The claim that the per-item distribution widens requires data beyond this table; omit unless explicitly sourced and needed.

For Table 2, add $d=16$ and define $\rho(D)$ as the spectral radius. Replace “full-rank and non-contractive ... yet never visited” with:

> $D$ is the complement block, with spectral radius $\rho(D)\geq1$. Nonzero cross-block leakage is reported explicitly; the decomposition does not establish an exactly invariant entity subspace.

A shorter, less editorial ending is simply to stop after the spectral-radius definition. The table's measurements already supply the limitation.

### 13. `sections/07_limitations.tex:77–99`: reproducibility and causal scope

Replace “md5-pinned raw artifacts” with “raw artifacts checked by MD5 hashes,” “rollups” with “aggregates,” and “back every number” with “support the reported measurements.”

The sentence “the necessity direction ... is robust to the cause of any individual sub-K collapse” is not supported: numerical instability can confound recovery differences. Suggested replacement preserving the archive's stated scope:

> The force-rank aggregate retains one recovery value per $(d,K,k)$ configuration and does not retain per-seed instability diagnostics. It therefore supports comparisons of aggregate recovery, but does not resolve the contribution of numerical failures to individual unsuccessful runs.

The registered falsifier at $d\geq32$ seems to concern the observed fixed-width recovery frontier, not the mathematical rank requirement. State the claim each counterexample addresses. Also define “ceiling” from the archived protocol; do not guess that it means the unrestricted reference.

Replace the last sentence with:

> Near-singular intermediate products produce BLAS \texttt{RuntimeWarning}s on some platforms. The analysis checks that every decomposition output is finite before use.

Finite outputs alone do not establish that numerical warnings have no effect on values, so omit “benign” and “do not affect any reported number” unless a separate validation supports them.

## Important items for root verification

1. Confirm the effective-rank implementation uses exponentiated entropy. This is a definition correction, not a new result.
2. Confirm the optimizer before retaining “plain SGD.”
3. Confirm the raw-input integrity test before labeling it a “gradient blank-out test.”
4. Do not retain zero-leakage or exact-empirical claims beside visibly nonzero residuals and a >0.9 threshold.
5. Preserve the rank theorem. The theorem concerns exact linear equality; the experiments concern a specified approximation threshold. Neither should be silently substituted for the other.
6. The numerical-instability caveat needs accurate scope; no new experiments are requested in this scrub.
7. Reproducibility says the artifacts accompany a repository release, but the manuscript contains no release URL. If a verified public release URL is already available, this is a useful addition. Do not invent or publish one as part of this audit.

**Verdict: FAIL (13 grouped wording/caption findings; zero mechanical banned-word, contraction, or author-voice violations).** The paper needs precision edits, not stylistic padding. Its numerical examples and theorem should remain unchanged.

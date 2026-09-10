# Fresh prose and precision recheck

Reviewed `source/main.tex` and all seven `source/sections/*.tex` files against the paper style judge and styleguide. This is a read-only source review; the source was not edited. The title is intentionally preserved for user review. Scientific claims were checked only for internal wording and notation consistency, without a new scientific review or authorship inference.

## Precision findings resolved during recheck

1. **Composition now defines a shared entity basis.** `source/sections/04_composition.tex:4–8` defines entity vectors, one-step bindings `k_i=e_i`, `v_i=e_{\pi(i)}`, depth target `e_{\pi^h(i)}`, and prediction `Z^h e_i`. This resolves the earlier inconsistency from reusing `v_i` both as a paired target and an entity vector. The parent verified the definition against the existing composition implementation at `task_e.py:29–30`.

2. **Effective rank is no longer described as sufficient algebraic rank.** `source/sections/05_frontier.tex:36–38` now concludes “High effective rank alone does not ensure accurate bindings.” This follows from the measured effective rank and recovery values without conflating the entropy metric with the algebraic rank in the exact-recovery inequality.

The abstract also now defines $K$ as the number of bindings, and `source/sections/07_limitations.tex:86–92` defines the reference recovery as that of a converged unconstrained model.

### Banned words

No hits in prose, captions, or headings. Checked the complete whole-word list from the styleguide, excluding source comments and citation keys.

### First-person / narrative-process

No violations. Editorial “we” describes the study and its findings without narrating the authors' research process.

### Contractions

No violations.

### Em-dash-as-pause

No violations. TeX double hyphens denote ranges or paired terms, not conversational em-dash pauses.

### Headings

No rhetorical-question headings.

### Captions

No non-self-contained captions. The recovery metric, experiment or comparison, and principal outcome are stated in each caption.

### Abstract length

202 whitespace-delimited tokens after removing evidence comments and TeX math delimiters and normalizing visible math commands. This matches the prior review's rendered-text-style counting convention and is within the 200–230 band.

### DO-NOT / apparatus

No violations. Parameter counts establish experimental scale and limitations; they are not apparatus boasts. No cost or funding claims appear.

### Anonymization

Not applicable: this is explicitly a named arXiv working draft. Author information is intentional.

## Precision checks that pass

- The exact-recovery inequality is explicitly conditional on linearly independent keys and values.
- The setup and abstract explicitly distinguish cosine greater than 0.9 from exact vector equality.
- Approximate composition is reported using measured recovery, residuals, and nonzero leakage; the intentionally retained title is outside this recheck's editing scope.
- Effective rank is correctly defined as exponentiated entropy, and rank caps are described as upper bounds.
- The depth-21 target repetition is explained, and the single converged rank-capped seed is disclosed.
- Abstract and body recovery values match the unchanged tables where those values overlap.

PASS (zero remaining essential prose or precision findings).

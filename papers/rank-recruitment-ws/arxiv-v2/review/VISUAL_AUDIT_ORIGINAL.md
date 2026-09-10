# Original companion PDF: visual inspection

Inspected the actual rendered PDF at `original/main.pdf`, pages 1–6, against six PNG renders. `pdfinfo` confirms six pages. Counts: **0 critical / 1 serious / 2 minor**. This render needs layout fixes before it is ready for the user's review. This is a named arXiv preparation, so no double-blind anonymity or separate venue page-limit check applies.

## Critical

None. All figures, tables, equations, and citations rendered; no visible unresolved reference markers, clipping, or unreadable margin overflow.

## Serious

1. **Pages 5–6: Appendix B is separated from its only content.** Page 5 ends with the heading “B Per-Seed Subspace Decomposition,” immediately followed by “C Reproducibility.” The table belonging to B appears at the top of page 6, between the first and second parts of C's opening paragraph. The apparent empty Appendix B and interruption of C make the structure hard to follow. Keep the Appendix B heading and Table 2 together, and place Appendix C after that table and its caption. This can be fixed by float placement/section boundaries; the table contents need no changes.

## Minor

1. **Page 5, Table 1: caption touches the bottom rule.** Add approximately one body-text line of vertical space between the table's bottom rule and its below-table caption, matching the user's stated spacing preference. Preserve normal separation between the completed caption and Appendix B.
2. **Page 6, Table 2: caption touches the bottom rule.** Apply the same caption spacing as Table 1.

## Page-by-page observations

- **Page 1:** Title, author block, abstract, keywords, and introduction fit within the text block. No clipped text or stranded heading.
- **Page 2:** Three-panel Figure 1 is legible at page scale. Axes, markers, dashed reference lines, and parameter labels render. Caption is adjacent. Sections 2–4 flow; Section 4 has several opening lines before the page break.
- **Page 3:** Figure 2 has readable axes, legends, and direct series labels. Markers/line styles supplement the colors. Caption is adjacent, with no clipping. Main text and headings fit. No need to regenerate plots on visual grounds.
- **Page 4:** Related work/limitations continuation and references render without margin problems.
- **Page 5:** Remaining bibliography and Appendix A fit. Table 1 caption needs more space. Appendix B heading is detached from its table, and Appendix C starts before that table; see serious finding.
- **Page 6:** Table 2 and caption render, but the caption needs more space. Appendix C continues beneath the misplaced float. Substantial bottom whitespace is not itself a defect for this short arXiv document.

**Pages inspected:** 1, 2, 3, 4, 5, 6 (all 6 of 6).

FAIL (3 findings)

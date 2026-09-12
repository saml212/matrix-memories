# Rank recruitment companion - arXiv submission staging

Final author-authorized publication cleanup, September 11, 2026. Final manuscript: source/main.tex; six-page PDF: source/main.pdf. FINAL_CHANGES.md summarizes the limited edits. FINAL_CONTENT_CHECK.md and FINAL_RENDER_CHECK.md record independent checks. VALIDATION.json and source-manifest.json identify the reviewed build.

The upload ZIP contains only 13 required TeX, bibliography, style, and figure files. Reviews, internal logs and this README are not uploaded. The public code/data repository is linked in Appendix C.

Submission 8069718 is created but not uploaded or submitted. User confirmation of the new arXiv agreement and CC BY 4.0 is pending through the question in the task. The author has already authorized manuscript cleanup and publication; do not ask for general publication approval again. Once agreement confirmation arrives, accept the agreement, choose CC BY 4.0 and cs.LG, upload ZIP, process, enter metadata.json, inspect arXiv-generated PDF, and submit. Verify final submitted status before reporting success.

Build on Mac mini from papers/rank-recruitment-ws/arxiv-v3:

```sh
/opt/homebrew/bin/tectonic --keep-logs --keep-intermediates main.tex
```

No new training or experiments. Existing archived outputs were rechecked.

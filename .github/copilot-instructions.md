# Copilot Instructions for Data Analysis Projects

## 1) Script Style and Execution

- Use a flat, top-to-bottom script style for analysis workflows.
- Avoid unnecessary function wrapping (`main()`, deeply nested helpers) unless reuse is required.
- Keep key intermediate objects in global scope for inspection and debugging.
- Organize scripts into short, executable blocks (load -> clean -> transform -> model -> summarize).

## 2) Reproducibility and Portability

- Set a random seed before any stochastic step.
- Never hardcode absolute local paths.
- Use relative paths or command-line arguments (`argparse` in Python, `commandArgs` in R).
- Prefer deterministic outputs (fixed sort order, explicit column order) when writing tables.

## 3) Observability During Transformation

- For complex transformations, print lightweight checks before and after:
	- shape / row count,
	- missing-value summary,
	- key distribution or basic summary stats.
- Keep checks simple so steps can be validated quickly during iterative work.

## 4) Comments and Libraries

- Write comments for WHY (method choice, threshold rationale, imputation strategy), not obvious WHAT.
- Prefer modern, maintained libraries:
	- Python: `pandas` or `polars`
	- R: `tidyverse`

## 5) Data Privacy and Mock Data

- Treat all data as sensitive clinical/biological data.
- Never use realistic patient identifiers in examples or mock data.
- Do not expose sensitive outputs in tracked files.

## 6) Directory and Git Safety Rules

- `data/`, `priv/`: read-only inputs. Never write outputs.
- `temp/`: intermediate artifacts and caches (gitignored).
- `log/`: execution logs and traces (gitignored).
- `output/`: detailed results, model artifacts, processed sensitive outputs (gitignored).
- `report/`: only de-identified, aggregated summaries and publication-safe plots/tables.

## 7) Plan-First and Approval Workflow

- Before making file changes, provide:
	- a short plan of intended edits,
	- target files,
	- expected impact.
- Explain changes first, then modify files.
- Ask for approval before edits unless the user has explicitly granted pre-approval for direct edits.
- If scope changes during implementation, pause and request confirmation before continuing.

## 8) Practical Recommendations

- Validate outputs after major steps (row counts, schema, key assumptions).
- Prefer writing intermediate data to `temp/` and final sensitive artifacts to `output/`.
- Keep Git-safe deliverables in `report/` only.

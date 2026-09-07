# Radiology-harness

Template-faithful radiology report generation for Natoe.ai hiring challenge (Kaggle private competition).

## Approach
- Treat `template_content` as starting report, not example.
- Route every dictated finding to matching FINDINGS field, minimally edit abnormal fields, preserve normals verbatim (RES-optimized).
- Update IMPRESSION concisely, no new info.
- Validate negation, laterality, measurements, field routing, preservation.
- LLM: Gemini 2.0 Flash (or GPT-4o-mini) via API, temperature 0, retry + deterministic fallback. Keys via env/secrets, never hardcoded.

## Files
- `generate.py` — complete automated pipeline (reads `test.csv`, writes `submission.csv`).
- `notebook.ipynb` — Kaggle Notebook version (share private with `natoeaidev`, paste URL in submission description).
- `PROMPT.md` — system prompt with field-preservation rules + chest example.
- `submission.csv` — 132 reports (`case_id,report`, FINDINGS+IMPRESSION only).
- `requirements.txt`

## Reproduce
```bash
export GEMINI_API_KEY='...'
python generate.py --input test.csv --output submission.csv --backend gemini --model gemini-2.0-flash
```

## Kaggle
1. Upload `submission.csv` via File Upload.
2. Upload `notebook.ipynb` as Kaggle Notebook, save version, share private with `natoeaidev`.
3. Paste notebook URL into Submission Description.

Leaderboard uses RES (lower better). Hiring review checks clinical faithfulness, routing, reproducibility, design separately.

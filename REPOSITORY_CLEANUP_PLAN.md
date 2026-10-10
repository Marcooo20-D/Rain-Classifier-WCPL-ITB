# Repository cleanup plan (review before merging)

## Observations
- `main.py`, `img_scraper.py`, and `color_checker.py` are in the repository root.
- `hasil.csv` and `hasil.png` are existing output files.
- Python bytecode is tracked in `__pycache__/`.
- `.github/workflows/daily_run.yml` runs `python main.py` and stages changes using `git add .`.
- `README.md` contains project information and an author credit; preserve attribution when editing it.
- The README mentions a 09:00 UTC schedule, while the current workflow uses `0 10 * * *` (10:00 UTC). Reconcile documentation with intended execution time.

## Proposed structure (not yet applied)
```
.
├── .github/workflows/daily_run.yml
├── src/
│   ├── main.py
│   ├── img_scraper.py
│   └── color_checker.py
├── data/
│   └── hasil.csv
├── figures/
│   └── hasil.png
├── README.md
├── requirements.txt
└── .gitignore
```

## Safe sequence
1. Verify that the GitHub Action still runs successfully on its existing paths.
2. Add `requirements.txt` with versions tested against the workflow's Python version.
3. Update the workflow if moving `main.py` to `src/`, and ensure Python imports still work.
4. Treat tracked `__pycache__/*.pyc` as candidates for untracking on a separate tested change; adding a `.gitignore` alone does not remove tracked files.
5. Decide whether `hasil.csv` contains an important historical series before relocating or untracking it. `hasil.png` may be a needed generated image.
6. Keep a backup and verify scheduled execution and the resulting CSV before merging.

**No existing file is deleted or moved by this plan.**

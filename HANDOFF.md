# Random Forest handoff

- The original September 19 snapshot generated exactly 1,444,267 cleaned entries, the same 50,000-row sample and the same 40,000/10,000 sex-stratified split.
- The existing Linear Regression code reproduced MAE 27.86 / 21.41 kg and RMSE 35.09 / 28.05 kg for bodyweight-only / full features. Source notebooks were not edited.
- EDA uses training data only. Forest A and B use the same split, F=0/M=1 encoding, five CV folds and RMSE selection rule. Both final forests were refitted on all training entries before test evaluation.
- `osama_work.ipynb` was executed from a fresh kernel and saved with all outputs. No test-driven retuning was performed.
- `report/Osama_report_sections.md` contains the exploration, method, results and limitations for review. Figure PNGs are in `results/figures/`. Use original PNGs rather than UI screenshots.
- `results/four_configuration_comparison.json` contains the verified existing Linear Regression results and new forest results for the joint comparison, which is now included in `main.ipynb`. The from-scratch Linear Regression implementation is preserved.
- Important limitation: 1,640 test entries have a name also present in training. The name audit is approximate; it does not identify unique athletes. Current results concern held-out entries, not necessarily new lifters. The agreed split was preserved.
- `ted_work.ipynb` and `osama_work.ipynb` were preserved during integration. `main.ipynb` is now the combined notebook and passed a fresh-kernel run of all 25 code cells with matching results. It has no dependency on the individual notebooks or pre-existing result files. Commits and pushes remain with the user.

- Authorship repair: all 44 cells from the latest referenced original notebook are preserved verbatim and in order in main.ipynb. See audit/source_preservation.json and audit/final_project_verification.json. The original introduction replaces the integration instructions. Report metrics were recomputed from saved test predictions and checked against shared targets.

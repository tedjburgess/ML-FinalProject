# Bench press prediction

## Current work

`osama_work.ipynb` contains training-data exploration and the two Random Forest configurations. Model A uses bodyweight; Model B uses bodyweight, age and recorded sex. `main.ipynb` contains the complete combined workflow and all four configurations. Both individual working notebooks are preserved unchanged by integration.

The work uses the September 19 OpenPowerlifting snapshot, the existing cleaning rules, a 50,000-entry sample with seed 42, and the existing 80/20 sex-stratified split with seed 42. Both Linear Regression results were reproduced from the original implementation to confirm data equivalence.

## Data and running

Keep `bench_press_sample.csv`, `bench_train.csv` and `bench_test.csv` beside the notebooks. The original CSV is under `Dataset/openpowerlifting-latest/openpowerlifting-2026-09-19/`, matching the existing preparation notebook. CSVs are local and ignored by Git.

Open the project folder as the notebook working directory, install `requirements.txt`, select that Python kernel, restart it, and run `main.ipynb` from the top. The combined notebook needs only the original snapshot and the Python packages; it regenerates the exported CSVs, provenance and results itself. Forest selection compares five settings using five training CV folds for each feature configuration. It may take several minutes. Test predictions are made after selection, and saved tables and plots are in `results/`.

`results/data_provenance.json` records original row IDs and the source hash. `results/shared_csv_sha256.json` records the three exported file hashes. These support checking the exact shared sample and split.

## Report and presentation

`report/Osama_report_sections.md` is a short draft of the exploration, forest method, results and limitations. It includes figure locations. Read it alongside the notebook and revise any wording before final integration. The notebook ends with presentation questions to help review how the model and evaluation work.

`HANDOFF.md` records the shared choices and integration status. The combined notebook includes one shared preparation and split, both model implementations, final evaluation, comparison and conclusion. No commits or pushes were made.

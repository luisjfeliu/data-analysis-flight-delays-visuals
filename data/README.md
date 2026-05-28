# Flight Delay Data

This project uses the Bureau of Transportation Statistics Reporting Carrier On-Time Performance Data for 2025.

## Tracked data

- `raw/On_Time_Reporting_Carrier_On_Time_Performance_1987_present_2025_*.zip`
  - Monthly BTS ZIP files for January through December 2025.
  - Tracked with Git LFS because the files are large binary source data.

## Local-only data

- `resources/` is intentionally ignored. It contains downloaded course materials, examples, and local extracted working files.
- `data/processed/` is intentionally ignored. Use it for generated files such as a combined CSV if you want a faster local reload path.

The notebooks can load directly from the tracked monthly ZIP files in `data/raw/`. If an ignored `data/processed/combined_2025.csv` exists locally, the notebooks will use it as a faster optional cache, so saved output may report the processed cache as its source. In a clean checkout without that cache, they load from the committed monthly ZIP files.

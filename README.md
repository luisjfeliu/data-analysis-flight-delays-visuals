# US Airlines On-Time Performance (2025)

## Dataset

**Source:** Bureau of Transportation Statistics — Reporting Carrier On-Time Performance Data
**Year:** 2025 (12 months: Jan–Dec)
**Size:** 7,001,619 scheduled flights across the monthly source ZIP files

The committed project data lives under `data/raw/` and is tracked with Git LFS. The `resources/` directory is intentionally ignored because it contains local course materials, example projects, and generated working files.

The notebooks load directly from the monthly ZIP files in `data/raw/`. If a local `data/processed/combined_2025.csv` exists, the notebooks use it as an optional faster cache; generated processed data should not be committed.

## Analysis Theme

Three interconnected questions drive the exploration:

1. **Q1 (Departure):** What factors most significantly influence flight departure delays?
2. **Q2 (Arrival):** What factors most significantly influence flight arrival delays?
3. **Q3 (Comparison):** How do the factors affecting departure delays differ from those affecting arrival delays?

This framing traces how delays accumulate (or get resolved) over the course of a flight. The Part II explanatory deck distills the exploration into five executive-summary insights about recovery, attributed causes, timing, seasonality, and geography.

## Part II Key Findings

1. **Flights often recover some schedule time after departure:** The median delay delta (ArrDelay - DepDelay) is negative, meaning completed flights tend to arrive closer to schedule than they departed. Large departure delays still have wider outcomes and are less predictable.

2. **Late aircraft and carrier delays lead attributed causes:** LateAircraftDelay and CarrierDelay are the largest contributors to attributed delay minutes, with NASDelay also meaningful. Weather and security delays are much smaller in the annual average.

3. **Sunday and late-day flights are most delay-prone:** Arrival-delay distributions and significant-delay rates peak on Sunday, especially in the evening, while Thursday and Friday evenings are also elevated and Tuesday is consistently lower.

4. **Seasonality has a summer peak and a December spike:** June and July show the highest significant arrival-delay rates, September is the clearest low-delay month, and December stands out as the strongest winter/holiday spike.

5. **Geography matters, but state aggregation is coarse:** Origin states differ in both average delay and departure-to-arrival recovery, but the largest recovery gaps are not always the same states with the highest mean delays.

Part I also found that distance alone is a weak predictor: significant arrival-delay rates are fairly flat across distance bins, so local factors such as airport congestion, weather, schedule timing, and airline operations appear more important than mileage by itself.

## Visualizations (19 total)

| # | Visualization | Type | Question |
|---|--------------|------|----------|
| V1 | DepDelay histogram | Histogram | How are departure delays distributed? |
| V2 | ArrDelay histogram | Histogram | How are arrival delays distributed? |
| V3 | DepDelay vs ArrDelay densities | KDE overlay | How do the distributions compare? |
| V4 | Distance histogram | Histogram | What is the distance distribution? |
| V5 | Mean delay by cause | Bar chart | What are the primary delay causes? |
| V6 | Flight completion status | Status bar chart | What proportion are cancelled/diverted? |
| V7 | DepDelay vs ArrDelay | Hexbin scatterplot | How do departure and arrival delays relate? |
| V8 | DepDel15 rate by airline | Ranked bar chart | Which airlines have worst departure performance? |
| V9 | ArrDel15 rate by airline | Ranked bar chart | Which airlines have worst arrival performance? |
| V10 | Significant delay flag overlap | Annotated heatmap | How often do significant departure and arrival delay flags overlap? |
| V11 | ArrDelay by day of week | Box plot | Do certain days have more delays? |
| V12 | ArrDel15 rate by month | Line chart | Are there seasonal patterns? |
| V13 | Distance vs ArrDel15 rate | Bar chart | Does distance relate to delay? |
| V14 | Delay causes by airline | Small-multiple bar chart | Do airlines experience different delay types? |
| V15 | Delay by day × time | Annotated heatmap | Are there day/time combinations with more delays? |
| V16 | DepDelay vs ArrDelay by state | Dumbbell plot | Do some states delay departures but recover en route? |
| V17 | Airline × distance delay comparison | Faceted scatter with color and size | How do airline, distance, and delay interact? |
| V18 | Delay delta analysis | Binned median/IQR plot | Do delays compound or dissipate? |
| V19 | Numeric correlation structure | Correlation heatmap | What is the correlation structure? |

## Files

- `Part_I_exploration.ipynb` — Main analysis notebook (executable)
- `Part_I_exploration.html` — Exported HTML report
- `Part_II_explanatory.ipynb` — Polished explanatory analysis notebook
- `Part_II_explanatory.slides.html` — Exported explanatory slide deck
- `data/raw/` — Monthly 2025 BTS source ZIP files tracked with Git LFS

## Methodology Notes

- **Status handling:** Cancelled and diverted flights are counted in status analysis but excluded from delay analysis because they do not have comparable completed-flight arrival outcomes.
- **NaN handling:** Blank delay-cause fields are converted to 0 because no minutes were attributed to that cause.
- **Subsampling and aggregation:** The hexbin scatterplot uses a 100K-row subsample, and several charts use grouped summaries to maintain performance with the 7M+ row dataset.
- **Airline grouping:** Top airlines by volume are analyzed individually where grouping is needed; smaller carriers are grouped as "Other".
- **Delayed threshold:** Official BTS `DepDel15` and `ArrDel15` flags are used for significant delays, meaning 15 minutes or more late.

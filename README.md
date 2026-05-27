# Part I: Exploratory Data Analysis — US Airlines On-Time Performance (2025)

## Dataset

**Source:** Bureau of Transportation Statistics — Reporting Carrier On-Time Performance Data
**Year:** 2025 (12 months: Jan–Dec)
**Size:** ~7 million flights (3 GB CSV, 109 columns)

## Analysis Theme

Three interconnected questions drive the exploration:

1. **Q1 (Departure):** What factors most significantly influence flight departure delays?
2. **Q2 (Arrival):** What factors most significantly influence flight arrival delays?
3. **Q3 (Comparison):** How do the factors affecting departure delays differ from those affecting arrival delays?

This framing traces how delays accumulate (or get resolved) over the course of a flight.

## Key Findings

1. **Delays compound over the flight:** The median delay delta (ArrDelay - DepDelay) is positive, meaning flights tend to arrive later relative to schedule than they departed. Late departures are particularly prone to worsening en route.

2. **Airline operations are the dominant delay driver:** LateAircraftDelay and CarrierDelay are the largest contributors to overall delays, suggesting airline operational efficiency (crew scheduling, aircraft turnaround, maintenance) is more impactful than weather or air traffic control.

3. **Friday is the worst day:** Both departure and arrival delays peak on Fridays, likely due to accumulated operational fatigue and end-of-week travel volume.

4. **Seasonal bimodality:** Delays are elevated in both winter (weather) and summer (thunderstorms + volume), with spring and fall showing the best on-time performance.

5. **Hub states drive congestion:** States with major hub airports (NY, FL, IL) show consistently higher delays, but the gap between departure and arrival delays varies — some hubs recover en route while others worsen.

6. **Distance is a weak predictor:** While longer flights tend to have slightly higher delays, the relationship is noisy. Local factors (airport congestion, weather) matter more than distance.

## Visualizations (18 total)

| # | Visualization | Type | Question |
|---|--------------|------|----------|
| V1 | DepDelay histogram | Histogram | How are departure delays distributed? |
| V2 | ArrDelay histogram | Histogram | How are arrival delays distributed? |
| V3 | DepDelay vs ArrDelay densities | KDE overlay | How do the distributions compare? |
| V4 | Distance histogram | Histogram | What is the distance distribution? |
| V5 | Mean delay by cause | Bar chart | What are the primary delay causes? |
| V6 | Flight status counts | Count plot | What proportion are cancelled/diverted? |
| V7 | DepDelay vs ArrDelay | Hexbin scatter | How do departure and arrival delays relate? |
| V8 | DepDelay by airline | Box plot | Which airlines have worst departure performance? |
| V9 | ArrDelay by airline | Box plot | Which airlines have worst arrival performance? |
| V10 | ArrDelay by day of week | Box plot | Do certain days have more delays? |
| V11 | ArrDelay by month | Box plot | Are there seasonal patterns? |
| V12 | Distance vs ArrDelay | Hexbin scatter | Does distance relate to delay? |
| V13 | Delay causes by airline | Clustered bar | Do airlines experience different delay types? |
| V14 | Delay by day × time | Facet plot | Are there day/time combinations with more delays? |
| V15 | DepDelay vs ArrDelay by state | Clustered bar | Do some states delay departures but recover en route? |
| V16 | Multi-encoding scatter | Scatter (color=size) | How do airline, distance, and delay interact? |
| V17 | Delay delta analysis | Scatter + box plot | Do delays compound or dissipate? |
| V18 | Pair plot | Scatter matrix | What is the correlation structure? |

## Files

- `Part_I_exploration.ipynb` — Main analysis notebook (executable)
- `Part_I_exploration.html` — Exported HTML report

## Methodology Notes

- **NaN handling:** NaN in delay columns represents on-time flights (0 delay), not missing data. All delay columns were filled with 0.
- **Subsampling:** Hexbin plots and pair plots used subsamples (50K–100K rows) to maintain performance with the 2M+ row dataset.
- **Airline grouping:** Top 10 airlines by volume analyzed individually; smaller carriers grouped as "Other".
- **Delayed threshold:** ArrDelay > 15 minutes used as the industry-standard definition of a delayed flight.

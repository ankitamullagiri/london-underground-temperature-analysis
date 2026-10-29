# London Underground Temperatures: Where to Pilot Air Cooling

A statistical analysis to recommend which London Underground line should trial a new air-cooling system, based on 12 years of monthly temperature readings.

**Context:** MSc Business Analytics, Warwick Business School (Business Statistics) · solo project · R

## Question

Acting as a policy maker: should the cooling pilot go on the **Bakerloo** or the **Central** line?

## Data

1,152 monthly average temperature readings (2013–2024) across Bakerloo, Central, Jubilee, Northern, Piccadilly, Victoria, Waterloo & City and the sub-surface lines.

| Column | Description |
|---|---|
| `Year`, `Month` | When the reading was taken |
| `Line` | Underground line |
| `Temp` | Average monthly temperature (°C) |

## Approach

1. **Data quality:** checked structure, missing values and outliers (histogram, boxplot, IQR rule).
2. **Cleaning:** set 6 physically implausible readings (below 5°C in summer, above 50°C, some over 200°C) to `NA` rather than dropping rows, after confirming this barely moved the mean (23.86 → 23.58°C). Excluded the sub-surface lines, which sit close to the surface and aren't comparable.
3. **Exploration:** violin plots with mean ± SD for each line.
4. **Inference:** Welch two-sample t-tests for Bakerloo vs Central, across the full year and for summer months only (May–August).

## Results

| Comparison | Bakerloo | Central | Test |
|---|---|---|---|
| All months | 26.82°C | 26.11°C | t = 2.18, **p = 0.03** |
| Summer (May–Aug) | 28.74°C | 28.68°C | t = 0.16, p = 0.87 |

Bakerloo is slightly but significantly warmer across the year. In summer, when cooling matters most, the two lines are statistically indistinguishable.

**Recommendation:** temperature alone doesn't separate the two lines at peak heat, so either is a reasonable pilot site. The decision should weigh passenger density, tunnel depth, existing ventilation, installation feasibility and cost.

## Run it

Open `underground_temperature_analysis.Rmd` in RStudio with `Underground.csv` in the same folder, then knit. Requires `tidyverse`, `lubridate`, `gridExtra` and `kableExtra`.

*The dataset was provided for the module and isn't included here.*

## Tech stack

R · tidyverse · ggplot2 · hypothesis testing

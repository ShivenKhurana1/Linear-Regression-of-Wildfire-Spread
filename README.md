# Wildfire Spread: A Regression Analysis of Weather Factors

**Can day-of weather predict how far a U.S. wildfire spreads?** A statistical study in R.

🏆 **1st Prize, Engineering and Physics**, Montgomery County Science Fair (2023) · **Top 300 Junior Innovators** nationwide, Thermo Fisher Scientific Junior Innovators Challenge

[Poster](https://drive.google.com/file/d/1KoEyi9jjwb_G6RkrR3U5nTXJfMkasEFt/view?usp=sharing) · [Poster PDF in repo](Finals/2023%20Montgomery%20Science%20Poster%20U.%20S.%20Wildfires%20FINAL-Shiven.pdf) · [Abstract](Finals/US%20Wildfires%20Science%20Fair%20Abstract-PDF.pdf)

## Why I built it

Wildfires cause deaths, respiratory and heart problems, property loss, worse air and water quality, carbon emissions and lasting damage to ecosystems. Research shows warmer, drier conditions are making them more frequent and larger in the western U.S. Predicting how a fire will spread is hard because so many factors interact, from fuel and terrain to the physics of heat transfer.

I wanted to test a simple question with real data: does the weather on the day a fire starts predict how far it spreads? If it did, it could support earlier warnings and prevention. I had just started learning R, so this project was also how I taught myself statistical modeling. The answer turned out to be mostly no, and working out why taught me more than a confirmed hypothesis would have.

## Hypothesis

Warm, dry and windy conditions significantly increase wildfire spread (area burned).

## Data

- 506 U.S. wildfire events, 2000 to 2009 (locations from latlong.net)
- Weather on the day of each fire from Weather Underground history: average temperature, high temperature, dew point, maximum wind speed, precipitation
- 2,500+ data points; outcome = log of area burned (hectares)

## Methods

Normality checks (histograms), IQR outlier removal on area burned, single-variable and multivariable linear regression (the multivariable model includes average temperature × high temperature and average temperature × wind interactions), and residual diagnostics in RStudio.

## Findings

- Of the five variables, only **high temperature** had a statistically significant relationship with spread (p = 0.031), and it was slightly *negative*: hotter days went with smaller fires in this sample. Average temperature was borderline (p = 0.054); precipitation, dew point and wind were not significant.
- The multivariable model had constant residual variance but violated normality, with several outliers.
- **The hypothesis was not supported.** A simple linear model is not enough to capture wildfire behavior, which depends on fuel, terrain and interacting weather effects.

## What I would do next

Try robust regression instead of trimming outliers; add recent fires and larger samples; add fuel, terrain and drought variables; use EPA and NASA data.

## Run it

The analysis is an R Markdown notebook that reads the dataset from the same folder:

- `Finals/WildFire-Projectcode.Rmd`: the full analysis
- `Finals/FINALWildFireData.xlsx`: 506 fires with location, date and weather

Open the `.Rmd` in RStudio and click **Knit**, or from a terminal:

```bash
cd Finals
Rscript -e 'rmarkdown::render("WildFire-Projectcode.Rmd")'
```

Needs the `readxl`, `dplyr` and `rmarkdown` packages. Saved plots are in `Histograms_Frequency/`, `Pair_Plots/`, `Residual_Plots/` and `Model Diagnostics/`.

## License

MIT. See [LICENSE](LICENSE).

# Victoria Road Accidents & Weather Impact Analysis

## Objective
To analyse the relationship between weather conditions and road traffic accidents in Victoria and assess how extreme heat events influence accident frequency.

## Data Sources
- Victorian road accident data (public dataset)
- Daily weather data (NOAA)

## Methodology
- Data cleaning and reshaping into tidy format
- Statistical distribution fitting (Poisson, Negative Binomial)
- Feature engineering using Excess Heat Factor (EHF)
- Regression modelling (Linear Models, GAM)
- Model comparison using AIC

## Key Insights
Data: daily accident counts for 7 Victorian regions, 1 Jan 2016 to 30 Jun 2020, joined to NOAA daily temperatures (Western region for the modelling).

**1. Accident counts are heavily overdispersed.** A Negative Binomial fit beats Poisson by a wide margin, so any count model of this data should not assume variance equals the mean.

| Distribution | Log-likelihood | AIC |
|---|---|---|
| **Negative Binomial** | **-69,393** | **138,790** |
| Geometric | -75,977 | 151,957 |
| Poisson | -113,153 | 226,307 |

**2. Heat on its own explains almost none of the day-to-day variation.** Excess Heat Factor has no detectable effect (p = 0.77, R² ≈ 0), and a GAM finds no non-linear effect either (deviance explained 0.005%). Daily temperature is statistically significant (p = 0.039) but tiny in size, about 0.002 fewer accidents per extra °C.

| Model | AIC |
|---|---|
| **Day temperature only** | **125,646.7** |
| EHF + day temperature | 125,648.5 |
| Intercept only (no weather) | 125,649.0 |
| GAM on EHF | 125,650.1 |
| EHF only | 125,650.9 |

**3. What this means.** Temperature alone is not enough to forecast accident-driven demand on emergency services. A useful model would need precipitation, visibility, day of week and holiday effects alongside temperature.

The full analysis with plots is in [`victoria-road-accidents-weather-analysis.html`](victoria-road-accidents-weather-analysis.html), and the R Markdown source is in [`notebooks/`](notebooks/).

## Tools
R, tidyverse, fitdistrplus, ggplot2

## Business Relevance
Insights from this analysis could assist emergency services in anticipating demand during extreme weather conditions.

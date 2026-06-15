<div align="center">

# Pouya Zargar

**Analytics engineer · Time-series econometrics · Marketing science**

I build measurement systems that survive contact with reality — bootstrap
CIs, Bayesian posteriors, the right unit of analysis, and the discipline
to call a negative result a negative result.

[![GitHub followers](https://img.shields.io/github/followers/Pouyasharp?label=Followers&style=flat-square)](https://github.com/Pouyasharp)
[![Public repos](https://img.shields.io/badge/repos-5-1f77b4?style=flat-square)](https://github.com/Pouyasharp?tab=repositories)
[![License: MIT](https://img.shields.io/badge/license-MIT-green?style=flat-square)](./LICENSE)

</div>

---

## What I work on

- **Marketing analytics** — Meta Ads measurement, price-test pipelines,
  weather-sensitivity analysis, end-to-end from data ingest to board deck.
- **Time-series econometrics** — ARIMA / ARIMAX / SARIMAX, unit-root
  testing, cointegration, lag analysis, structural breaks.
- **Causal inference** — DiD, IV, synthetic control, RDD; the discipline
  to know when a regression is descriptive and stop there.
- **ML+causal** — double/debiased ML, causal forests (econml, dowhy).

The throughline: I care more about whether the model is *right* than whether
it ships. The "excellent and robust" part is the part I find most fun.

---

## Featured projects

<table>
<tr>
  <td width="50%">

### [meta-price-test-analysis](https://github.com/Pouyasharp/meta-price-test-analysis)

A 3-stage Meta Ads price-test analysis pipeline. For each city it runs:

1. **Stage 1** — Bootstrap 10k daily-mean draws for ROAS / CVR, SARIMAX
   60-day revenue forecast with CI
2. **Stage 2** — Welch's t-test + Cohen's *d* for effect size
3. **Stage 3** — Bayesian posterior on the ROAS difference, Monte Carlo
   win-probability, power curve (log-y)

Synthesis rule (called a winner when 2 of 3 hold):
- Bayesian `P(treat > ctrl) > 0.95`
- MC `P(treat > ctrl) > 0.70`
- `|Cohen's d| > 0.2`

Built for 5 US cities (Baton Rouge, Sunset Beach, Reading, Cleveland,
Burnsville), 10 viz total.

</td>
  <td width="50%">

### [poseidon-weather](https://github.com/Pouyasharp/poseidon-weather)

A small library + analysis for joining ad-performance data with
Open-Meteo historical weather, then correlating / lagging / regressing
the two.

- `weather.py` — Open-Meteo historical fetcher (cached)
- `join.py` — long-form ad panel + weather merge
- `correlate.py` — Pearson r + p per (show, city)
- `lag.py` — lagged correlations, best-lag picker
- `regression.py` — OLS with DOW + city FE
- `viz.py` — heatmap, lag curve, scatter-with-fit

Includes a runnable example on synthetic data with **planted weather
effects** so you can verify the library actually finds them.

</td>
</tr>
<tr>
  <td>

### [arimax-sarimax-tutorial](https://github.com/Pouyasharp/arimax-sarimax-tutorial)

PhD-level deep-dive curriculum on three pillars of applied time-series
econometrics: nonstationarity, ARIMAX, SARIMAX.

- **790-line `SKILL.md`** — Wold (1938), ADF, KPSS, PP, Perron, Zivot-Andrews,
  HEGY, Box-Jenkins-Tiao transfer functions, intervention analysis,
  Granger causality, endogeneity trap and IV fix
- **5 self-contained Python demos** (~1,500 LOC) — nonstationarity,
  ARX/IV/Granger, SARIMAX, residual diagnostics, full Schenectady-style
  capstone
- **290-line statsmodels API quirks reference** — things that bit me
  across statsmodels versions and would bite you too
- **Self-assessment rubric** (12 items) and **21-paper reading list**

  </td>
  <td>

### Stack

| Layer | Tools |
|---|---|
| Languages | Python, SQL, a working knowledge of R |
| Estimation | `statsmodels`, `scipy`, `linearmodels`, `econml`, `dowhy` |
| Time series | `statsmodels.tsa`, `pmdarima`, `arch` |
| Bayesian | `pymc`, custom posteriors over bootstrap draws |
| Causal | DiD, IV, RDD, synthetic control, DML |
| Data | pandas, polars, parquet, postgres / supabase |
| API | FastAPI, Next.js (for client-facing analytics) |
| Weather | Open-Meteo Historical Weather API |
| Plotting | matplotlib (deterministic, deck-ready PNGs) |

</td>
</tr>
</table>

---

## Currently

- **Reading:** Box & Jenkins (1976) *Time Series Analysis* end-to-end,
  with a focus on the identification recipes that predate the
  auto_arima era
- **Building:** tighter unit-of-analysis discipline into the next
  Meta price-test report — `(show, city, ad-set)` not just `(show, city)`
- **Curating:** a PhD-level econometrics curriculum (5 stages, top to
  bottom), with deep-dives on the topics most often needed in applied
  marketing analytics

---

## How I work

- **Negative results are results.** A rejected hypothesis is a clean
  answer, not a failure of the experiment. The poseidon-weather
  methodology doc has a whole section on the three negative results
  that came out of the real analysis.
- **The right unit of analysis is everything.** National correlations
  hid opposite-signed city effects in the poseidon study. Always
  stratify first, then look at the average.
- **Bootstrap before you believe.** A point estimate without a CI is
  half a result. The `meta-price-test-analysis` pipeline computes
  10k bootstrap draws by default — the price of running it is small,
  the price of skipping it is large.
- **Controls dominate.** Day-of-week and city fixed effects routinely
  move point estimates by 30–50% in the ad-performance world. No
  weather / price / seasonal analysis ships without them in my work.

---

## Get in touch

The fastest way is GitHub — open an issue on any of the repos above
or DM `@Pouyasharp` on X.

<div align="center">

<sub>Built with care · Last updated 2026-06-15</sub>

</div>

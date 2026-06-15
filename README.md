<div align="center">

# Pouya Zargar

**Analytics engineer · Time-series econometrics · Marketing science · Agentic systems**

I build measurement systems that survive contact with reality — bootstrap
CIs, Bayesian posteriors, the right unit of analysis, and the discipline
to call a negative result a negative result.

[![GitHub followers](https://img.shields.io/github/followers/Pouyasharp?label=Followers&style=flat-square)](https://github.com/Pouyasharp)
[![Public repos](https://img.shields.io/badge/repos-14-1f77b4?style=flat-square)](https://github.com/Pouyasharp?tab=repositories)
[![License: MIT](https://img.shields.io/badge/license-MIT-green?style=flat-square)](./LICENSE)

</div>

---

## What I work on

- **Marketing analytics** — Meta Ads measurement, price-test pipelines,
  weather-sensitivity analysis, end-to-end from data ingest to board deck.
- **Time-series econometrics** — ARIMA / ARIMAX / SARIMAX, unit-root
  testing, cointegration, lag analysis, structural breaks.
- **Causal inference** — DiD, IV, synthetic control, RDD, PSM, DML;
  the discipline to know when a regression is descriptive and stop there.
- **Agentic systems** — ReAct, Plan-and-Execute, human-in-the-loop
  approval flows, confidence-gated action generation.

The throughline: I care more about whether the model is *right* than
whether it ships. The "excellent and robust" part is the part I find
most fun.

---

## Featured projects

### 📊 Marketing analytics

<table>
<tr>
  <td width="50%">

#### [meta-price-test-analysis](https://github.com/Pouyasharp/meta-price-test-analysis)

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

#### [meta-price-campaign-analysis](https://github.com/Pouyasharp/meta-price-campaign-analysis)

**Process documentation** for the price-test workflow:

- 3 references: bootstrap-on-ratios, Meta export column-index trap,
  SARIMAX model selection for short series
- The 3-test rule (always run all three)
- A reusable `analyze_template.py` (path-portable)

The companion to `meta-price-test-analysis` (the code) — this is the
*how and why*, that one is the *what it produces*.

</td>
</tr>
<tr>
  <td>

#### [poseidon-weather](https://github.com/Pouyasharp/poseidon-weather)

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
effects** so you can verify the library actually finds them. Plus the
6 final figures from the real 3-show × 5-city analysis in `results/`.

</td>
  <td>

#### [docx-report-generation](https://github.com/Pouyasharp/docx-report-generation)

Playbook for generating professional Word documents with `python-docx`:

- The 3 mandatory pitfalls (table dimensions, add_run style, run.bold)
- 10-section audit/comparison report structure
- Color coding convention (IMPROVING / CONCERNING / CRITICAL)
- Verification-first workflow
- Telegram document delivery (the silent-drop trap)

The methodology that backs the 5 DOCX reports shipped with
`poseidon-weather`.

</td>
</tr>
</table>

### 🧠 Econometrics

<table>
<tr>
  <td width="50%">

#### [econometrics-deep-research](https://github.com/Pouyasharp/econometrics-deep-research)

A PhD-level 5-stage econometrics curriculum (Yale / Georgia Tech depth):

- **Stage 1** — Foundations: probability, asymptotics, LLN/CLT, sandwich SE, bootstrap
- **Stage 2** — Classical: OLS, GLS, GMM, M-estimation
- **Stage 3** — Time series: unit roots, cointegration, GARCH, structural breaks
- **Stage 4** — Panel & causal: FE, IV, DiD, RDD, PSM, synthetic control
- **Stage 5** — Modern frontiers: DML, causal forests, Bayesian, structural

Includes 6 runnable Python demos (Stage 1 foundations + 5 time-series),
4 reference docs, self-assessment rubrics, and a 21-paper reading list.

</td>
  <td width="50%">

#### [arimax-sarimax-tutorial](https://github.com/Pouyasharp/arimax-sarimax-tutorial)

PhD-level **deep-dive** on the time-series half of the curriculum:

- 790-line `SKILL.md` — Wold (1938), ADF, KPSS, PP, Perron, Zivot-Andrews,
  HEGY, Box-Jenkins-Tiao transfer functions, intervention analysis,
  Granger causality, endogeneity trap and IV fix
- 5 self-contained Python demos (~1,500 LOC) — nonstationarity,
  ARX/IV/Granger, SARIMAX, residual diagnostics, full Schenectady-style
  capstone
- 290-line statsmodels API quirks reference
- Self-assessment rubric (12 items) and 21-paper reading list

The standalone deep-dive of the time-series stage in
`econometrics-deep-research`.

</td>
</tr>
<tr>
  <td>

#### [causal-inference](https://github.com/Pouyasharp/causal-inference)

PhD-level **deep-dive** on the causal-inference half of Stage 4:

- 440-line `SKILL.md` — IV / 2SLS (with first-stage F, AR CI, Sargan J),
  DiD (with the TWFE pathology and modern estimators), RDD (local-linear
  with IK bandwidth, donut-hole), PSM (with balance checks and
  Abadie-Imbens SEs), Synthetic Control (with in-space placebos), DML
  (with 5-fold cross-fitting)
- 5 self-contained Python demos (~1,500 LOC) with **planted effects** so
  you can verify each estimator recovers the truth
- statsmodels / linearmodels / dowhy / econml gotcha bank
- 8-item self-assessment rubric + 15-paper reading list

</td>
  <td>

#### [cointegration-vecm](https://github.com/Pouyasharp/cointegration-vecm) · [garch-volatility](https://github.com/Pouyasharp/garch-volatility) · [panel-data-causal](https://github.com/Pouyasharp/panel-data-causal)

Three PhD-level deep-dives on the technical corners of Stage 3 and 4:

- **`cointegration-vecm`** (v0.2.0) — 5 demos on the cointegration half
  of Stage 3: Engle-Granger 2-step, Johansen trace test, VECM
  estimation, Granger causality in VECM (weak + strong exogeneity),
  Gregory-Hansen structural breaks
- **`garch-volatility`** (v0.2.0) — 5 demos on the volatility half
  of Stage 3: GARCH(1,1), GJR-GARCH (leverage + News Impact), EGARCH
  (log-vol), DCC (time-varying correlation), VaR backtest (Kupiec +
  Christoffersen)
- **`panel-data-causal`** (v0.2.0) — 5 demos on the panel half of
  Stage 4: FE/RE/Hausman, two-way FE + cluster-robust SE, Arellano-Bond
  GMM (Nickell bias), Mundlak correction, Hausman-Taylor (manual 2SLS)

Each ships ~500-600 line `SKILL.md`, INDEX.md, REFINEMENT.md, and a
package-specific gotcha bank.

</td>
</tr>
</table>

### 🤖 Agentic systems

<table>
<tr>
  <td width="100%">

#### [amiq-deep-agent-layer](https://github.com/Pouyasharp/amiq-deep-agent-layer)

**Portfolio writeup** of the deep-agent architecture I designed and
shipped for the [AMIQ](https://github.com/sobhanb-eth/ads-marketing-iq)
platform (Ads & Marketing IQ, owned by Sobhan Bahrami). 3,693 lines of
agent code, all upstream.

- **ReAct** single-agent + **Plan-and-Execute** three-stage
- **Strategy Agent** with confidence-gated action generation
- **Human-in-the-loop pending-actions API** — every strategy proposal
  is stored, surfaced, and *requires explicit human approval* before
  any writeback
- **Streaming protocol** so the dashboard can show LLM tokens, tool
  calls, and tool observations in real time
- Built on LangChain 1.2.x's `create_agent` (returns a
  `CompiledStateGraph` directly — no `AgentExecutor`)

**Honest about what I did and didn't do:** the writeup explicitly
calls out "no writebacks to Meta/Google APIs in Phase 3", "no custom
agent loop", "no fine-tuning" — operational discipline matters more
than architectural novelty.

</td>
</tr>
</table>

---

## Stack

| Layer | Tools |
|---|---|
| Languages | Python, SQL, a working knowledge of R, TypeScript (for the AMIQ dashboard) |
| Estimation | `statsmodels`, `scipy`, `linearmodels`, `econml`, `dowhy` |
| Time series | `statsmodels.tsa`, `pmdarima`, `arch` |
| Bayesian | `pymc`, custom posteriors over bootstrap draws |
| Causal | DiD, IV, RDD, synthetic control, DML |
| Agentic | LangChain 1.2.x, LangGraph, ReAct, Plan-and-Execute, HITL approval flows |
| Data | pandas, polars, parquet, postgres / supabase |
| API | FastAPI, Next.js (for client-facing analytics) |
| Weather | Open-Meteo Historical Weather API |
| Plotting | matplotlib (deterministic, deck-ready PNGs) |
| Reporting | `python-docx`, structured audit reports |

---

## Currently

- **Reading:** Box & Jenkins (1976) *Time Series Analysis* end-to-end,
  with a focus on the identification recipes that predate the
  `auto_arima` era
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
- **Confidence gating on agent actions.** Below 0.50, refuse to act
  and surface data-quality issues instead. Above 0.50, propose with
  explicit human approval. The pending-actions table is the path of
  least resistance for review.

---

## Get in touch

The fastest way is GitHub — open an issue on any of the repos above
or DM `@Pouyasharp` on X.

<div align="center">

<sub>Built with care · Last updated 2026-06-15 · 12 active repos (3 scaffold-deepened today, 1 writeup, 4 marketing, 5 econometrics) · 2 archived (2023)</sub>

</div>

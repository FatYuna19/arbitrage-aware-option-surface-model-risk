# Arbitrage-Aware Option-Surface Construction and Model-Risk Analysis

A research pipeline for constructing, repairing, and evaluating an empirical SPY implied-volatility surface.

The project progresses from no-arbitrage pricing foundations to empirical option-chain processing, static-arbitrage diagnostics, SVI/SSVI surface repair, and Heston/Bates calibration.

The central question is not simply:

> Which model produces the lowest calibration error?

It is:

> What role has each model actually earned the right to perform?

The final result is deliberately conservative. For the single SPY option-chain date studied, a repaired simple implied-volatility surface remains the preferred representation of the market surface. Bates provides useful parametric diagnostics and stress-testing capability, but does not earn final pricing or representation authority. Heston is retained as a negative control rather than presented as a successful final model.

---

## Research objective

Complex models often fit option data better than simpler alternatives, but improved fit does not automatically justify greater modeling authority.

This project evaluates the full workflow behind an empirical volatility surface:

1. establish no-arbitrage pricing foundations;
2. ingest and clean market option quotes;
3. recover implied volatilities;
4. identify static-arbitrage violations;
5. construct a repaired surface;
6. calibrate stochastic-volatility and jump models;
7. compare fit, residual behavior, stability, and practical limitations;
8. assign each model an appropriate use rather than selecting a winner solely by complexity.

The project therefore treats calibration as a model-risk problem, not merely an optimization problem.

---

## Final research conclusion

For the market snapshot examined:

* The **repaired simple implied-volatility surface** is the preferred surface representation.
* The **Bates model** materially improves upon Heston and is useful for diagnostics, structural interpretation, and stress testing.
* Bates does **not** outperform the strongest simple surface baseline on implied-volatility RMSE.
* The **Heston model** fails the final empirical hurdles and is retained as a negative control.
* Neither calibrated stochastic model is granted production-pricing authority.
* No claim of temporal out-of-sample robustness is made because the empirical study uses a single option-chain date.

The main conclusion is therefore:

> Complexity earned diagnostic value, not pricing authority.

---

## Recommended reading order

Readers do not need to begin with Notebook 01.

### For a concise review

1. **Notebook 13 — Research Synthesis and Final Report**
   Consolidates the evidence, freezes the final claims, and states the project’s use policy.

2. **Notebook 12 — Model Calibration, Validation, and Surface-Risk Diagnostics**
   Contains the Heston/Bates comparison, calibration assessment, residual analysis, and final model-risk decision.

3. **Notebook 11 — Arbitrage-Aware SVI/SSVI Surface Repair and Handoff**
   Constructs the repaired empirical surface used by the downstream calibration analysis.

### For the complete technical progression

Read Notebooks 01 through 13 in sequence.

---

## Notebook structure

| Notebook                                                                | Purpose                                                                                           |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `01_binomial_no_arbitrage_replication.ipynb`                            | Establishes replication and no-arbitrage pricing foundations using binomial models.               |
| `02_brownian_motion_gbm_and_quadratic_variation.ipynb`                  | Develops Brownian motion, geometric Brownian motion, and quadratic-variation foundations.         |
| `03_ito_lemma_and_black_scholes_pde.ipynb`                              | Connects Itô calculus to the Black-Scholes partial differential equation.                         |
| `04_black_scholes_formula_greeks_and_numerical_checks.ipynb`            | Implements Black-Scholes pricing, Greeks, and numerical consistency checks.                       |
| `05_risk_neutral_monte_carlo_and_delta_hedging_error.ipynb`             | Examines risk-neutral Monte Carlo pricing and discrete delta-hedging error.                       |
| `06_implied_volatility_inversion_and_no_arbitrage_bounds.ipynb`         | Implements implied-volatility inversion subject to option-price bounds.                           |
| `07_static_arbitrage_diagnostics_for_option_surfaces.ipynb`             | Introduces static-arbitrage diagnostics for volatility surfaces.                                  |
| `08_spy_option_chain_ingestion_and_quote_filtering.ipynb`               | Ingests and filters empirical SPY option-chain data.                                              |
| `09_SPY Implied Volatility Inversion and Surface-Grade Filtering.ipynb` | Produces surface-grade implied-volatility observations from filtered quotes.                      |
| `10_raw_static_arbitrage_diagnostics_for_spy_iv_surface.ipynb`          | Audits the raw empirical surface for calendar, monotonicity, convexity, and related violations.   |
| `11_arbitrage_aware_svi_ssvi_surface_repair_and_handoff.ipynb`          | Fits and evaluates SVI/SSVI-style repairs and constructs the selected downstream surface handoff. |
| `12_model_calibration_validation_and_surface_risk_diagnostics.ipynb`    | Calibrates Heston and Bates, evaluates fit and residual behavior, and assigns model authority.    |
| `13_v1_1_research_synthesis_and_final_report.ipynb`                     | Consolidates the final evidence and presents the frozen research conclusions.                     |

---

## Research workflow

### 1. Pricing foundations

The early notebooks reproduce the mathematical and numerical foundations required for the empirical analysis:

* no-arbitrage replication;
* binomial option pricing;
* Brownian motion and geometric Brownian motion;
* Itô’s lemma;
* the Black-Scholes PDE;
* Black-Scholes pricing and Greeks;
* risk-neutral Monte Carlo;
* discrete delta-hedging error.

These notebooks establish internal consistency before the project moves to market data.

### 2. Implied-volatility recovery

Market option prices are converted into implied volatilities only after checking admissible pricing bounds and numerical inversion behavior.

The pipeline distinguishes between:

* a mathematically invertible quote;
* a liquid or economically meaningful quote;
* an observation suitable for surface construction.

This prevents raw option-chain availability from being confused with usable surface data.

### 3. Quote filtering and empirical surface construction

The SPY option chain is filtered to remove or flag observations that are unsuitable for surface analysis.

The objective is not to preserve every quote. It is to construct a defensible empirical panel while retaining a clear record of the data funnel and exclusions.

### 4. Static-arbitrage diagnostics

The raw empirical surface is audited for violations such as:

* option-price monotonicity failures;
* strike convexity failures;
* calendar inconsistencies;
* unstable or implausible implied-volatility observations;
* surface behavior that is incompatible with a defensible pricing representation.

The diagnostics are treated as empirical evidence, not merely preprocessing warnings.

### 5. SVI/SSVI repair

The project evaluates arbitrage-aware parametric surface repair and compares candidate handoffs.

The selected repaired surface is not assumed to be correct merely because it is smoother. It must improve structural consistency while remaining empirically faithful to the observed market snapshot.

### 6. Heston and Bates calibration

Heston and Bates models are calibrated against the repaired empirical target.

The comparison considers more than optimizer success:

* implied-volatility fit;
* option-price fit;
* residual structure;
* parameter plausibility;
* stability and fairness of the comparison;
* whether the additional jump component earns measurable value;
* whether either model improves upon the simpler surface representation.

Bates performs materially better than Heston, indicating that jump dynamics contain useful diagnostic information for this snapshot. However, its improvement over Heston does not establish superiority over the best simple repaired surface.

### 7. Model-risk synthesis

The final stage separates three possible roles:

1. **Surface representation**
   What should represent the observed implied-volatility surface?

2. **Structural diagnostics**
   What model helps interpret volatility, correlation, and jump behavior?

3. **Production pricing**
   What model has enough validation to support repeated operational use?

The project grants these roles separately rather than assuming one calibrated model should receive all three.

---

## Final use policy

### Repaired simple surface

Use for:

* representation of the studied market surface;
* descriptive analysis;
* comparison against calibrated structural models.

### Bates model

Use for:

* parametric diagnostics;
* jump-risk interpretation;
* scenario analysis;
* stress testing;
* comparison against Heston.

Do not treat it as the final empirical surface representation.

### Heston model

Use as:

* a benchmark;
* a negative control;
* evidence that stochastic-volatility complexity alone was insufficient for this snapshot.

Do not use it as the final calibrated model.

### Production use

Not authorized.

The project does not establish:

* temporal out-of-sample performance;
* calibration stability across dates;
* live quote reliability;
* production-grade numerical resilience;
* hedging superiority;
* robustness across instruments or market regimes.

---

## Scope and limitations

This is a research and model-risk study based on a **single SPY option-chain date**.

The conclusions are intentionally limited to that setting.

Important limitations include:

* no multi-date walk-forward calibration study;
* no claim of temporal out-of-sample robustness;
* no production execution or live-pricing system;
* no demonstrated hedging advantage for Heston or Bates;
* no claim that the selected surface repair is universally optimal;
* no validation across different underlyings or market regimes;
* dependence on quote quality and filtering choices;
* calibration sensitivity to objective functions, bounds, initialization, and numerical implementation.

A successful optimizer is not treated as proof of a successful model.

---

## Reproducibility

This repository is primarily an **audit and research archive**, not a packaged clone-and-run application.

The notebooks preserve the completed workflow and recorded outputs, but:

* raw and intermediate market data are not included;
* some notebooks use local project paths;
* rerunning may require path changes;
* dependencies may need to be installed manually;
* replacement option-chain data may not reproduce the same empirical results;
* later notebooks depend on artifacts created by earlier stages of the pipeline.

Readers interested in the conclusions should begin with Notebook 13. Readers interested in auditing the surface repair and calibration decisions should continue with Notebooks 11 and 12.

---

## Repository purpose

This repository is intended for:

* methodological review;
* quantitative-finance portfolio evaluation;
* derivatives-pricing study;
* model-risk discussion;
* audit of the reasoning behind the final model hierarchy.

It is not intended as:

* investment advice;
* a trading strategy;
* a production option pricer;
* a live volatility-surface service;
* evidence that Bates or Heston will perform reliably outside the studied snapshot.

---

## Project status

Version: **v1.1**

The current research cycle is complete.

Future work would require a materially broader validation design, including repeated option-chain dates, rolling or walk-forward calibration, parameter-stability analysis, hedging evaluation, and market-regime comparisons. Those extensions are outside the claims of the present repository.

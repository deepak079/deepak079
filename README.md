<p align="center">
  <img src="assets/banner.svg" alt="Deepak Singh: Quantitative Modeling & Research" width="100%">
</p>

<!-- TODO: one line on your current role or program, e.g. "MS student at … / Quant researcher at …" -->

## 🧭 Research Interests

- **Sequential decision-making and online learning:** stochastic control, reinforcement learning and adaptive
  control, with a focus on exploration and learning dynamics in these settings.
- **Statistical modeling and inference:** how the estimation target and assumptions about the data-generating
  process guide the choice of models and estimators. I'm interested in robustness to model misspecification
  and finite-sample performance, especially for nonparametric and high-dimensional methods: kernel methods,
  low-rank estimation and random matrix theory.
- **Applications in quantitative finance:** alpha discovery, dynamic portfolio construction, derivatives pricing,
  and optimal quoting in market making.

I'm currently exploring **neural PDE methods for stochastic control** and **computational methods for inference**.

---

## 🔬 Recent Work

### Fear of falling behind: a mean-field game of portfolio choice

<img src="assets/wealth_dynamics.gif" width="560" alt="Wealth distribution and risky holdings over one year, with and without peer concern">

*How does a crowd of investors invest when each one fears ending the year below the average?*

Each investor chooses how much to put in a risky asset and is penalised for ending below the
population's average wealth. That average is itself the result of everyone's choices, so the
problem is a **mean-field game**: an HJB equation for each investor's best strategy, a
Fokker–Planck equation for how the population's wealth evolves, and a fixed point where the
average investors plan against is the average they produce. It has the same structure as
heterogeneous-agent macro models (Aiyagari; Achdou, Han, Lasry, Lions & Moll), with peer
comparison in place of an interest rate.

**What we did**
- Found that the problem as originally posed let peers have no effect on anyone's choices, and
  redesigned the penalty so individual strategies and the crowd shape each other.
- Built finite-difference solvers for both equations and the equilibrium search as the benchmark,
  with errors of about 10⁻⁶ (checked against the exact no-penalty solution and by grid
  refinement).
- Solved the same system with **physics-informed neural networks** (PyTorch), matching the
  benchmark equilibrium to 0.014%.

**What it shows**
- Investors near the average cut their risky holdings to about a third of the no-peer level, so
  wealth piles up just below the average.
- The population's average one-year return falls from **11.0% to 6.5%**: competing on relative
  performance costs everyone return.
- The result barely depends on what investors expect: any belief about the average between 1.0
  and 1.3 leads to a realised average between 1.059 and 1.070.

`Python` · `PyTorch` · `NumPy/SciPy` · finite differences · PINNs · AMS 516, Stony Brook · joint work with Ander Ibarrondo

---

### Safe leverage for crypto perpetual futures

<img src="assets/rate_vs_leverage.png" width="760" alt="Liquidation rate vs average leverage for six forecasting methods, long and short, at 1% and 5% targets">

*How much leverage can you take on a crypto perpetual future and still keep the chance of liquidation at 1%?*

Under isolated margin, a position at leverage `L` is liquidated when its worst adverse move in the
holding window reaches `1/L − mmr` (mmr: maintenance margin rate). So safe leverage follows from a
forecast of the α-quantile of that move: `L = 1/(mmr + |q̂_α|)`. We compared ways of forecasting it on
7 Binance perpetuals (about 36,000 8-hour windows, 2022–2026), out of sample over 51 monthly refits.

**What we did**
- Built a data pipeline from Binance's public archive and a walk-forward harness, and evaluated
  liquidation rates with Kupiec and Christoffersen tests.
- Compared six forecasting rules: historical quantile, OLS with normal errors, GARCH(1,1)-t,
  quantile regression, kernel-weighted quantile and CVaR regression.
- Fitted quantile regression pooled across coins with coin fixed effects on four market-state
  factors (funding, open-interest change, realized volatility, basis), using PSG.

**What it shows**
- Pooled quantile regression met the 1% target for longs (1.00% liquidated, all 7 coins within
  Kupiec bounds) at **14% more leverage** than the standard historical-quantile rule.
- A normal tail is too thin: OLS liquidates 2.6–3.3% at a 1% target. GARCH-t buys its leverage
  with extra liquidations.
- A nonparametric kernel model did not beat linear quantile regression.
- CVaR regression is deliberately conservative: well below target, at a quarter to a third less leverage.
- Limitations: at 1% short every method liquidates too often; liquidations cluster in time; fees and
  funding are excluded.

<details>
<summary>Full results: liquidation rate / average leverage, out of sample</summary>

| Method | 1% long | 1% short | 5% long | 5% short |
|---|---|---|---|---|
| Historical quantile | 1.23% / 12.8× | 1.27% / 12.9× | 5.01% / 20.7× | 5.16% / 21.2× |
| OLS, normal errors | 2.60% / 17.8× | 3.30% / 18.9× | 4.81% / 22.1× | 5.75% / 23.4× |
| GARCH(1,1)-t | 1.38% / 15.3× | 1.12% / 14.5× | 6.11% / 24.8× | 5.75% / 24.1× |
| **Quantile regression** | **1.00% / 14.5×** | 1.35% / 15.3× | 4.76% / 23.6× | 5.31% / 23.9× |
| Kernel-weighted quantile | 1.14% / 13.7× | 1.35% / 14.1× | 5.08% / 22.9× | 5.59% / 23.2× |
| CVaR regression | 0.41% / 10.6× | 0.48% / 11.6× | 1.43% / 16.1× | 1.83% / 17.0× |

</details>

`Python` · `statsmodels` · PSG · quantile regression · GARCH · CVaR · AMS 518, Stony Brook · joint work with Marcus Minutello

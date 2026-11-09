<p align="center">
  <img src="assets/banner.svg" alt="Deepak Singh: Quantitative Modeling & Research" width="100%">
</p>

I work on quantitative models for markets: portfolio construction, statistical arbitrage, market microstructure and regime detection.

<!-- TODO: one line on your current role or program, e.g. "MS student at … / Quant researcher at …" -->

---

## 🔬 Recent Projects

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

**What I did**
- Found that the problem as originally posed let peers have no effect on anyone's choices, and
  redesigned the penalty so individual strategies and the crowd shape each other.
- Built finite-difference solvers for both equations and the equilibrium search, accurate to one
  part in a million, as the benchmark.
- With a teammate, solved the same system with **physics-informed neural networks** (PyTorch):
  I built the Fokker–Planck network and the equilibrium search. The networks match the benchmark
  equilibrium to 0.014%.

**What it shows**
- Investors near the average cut their risky holdings to about a third of the no-peer level, so
  wealth piles up just below the average.
- The population's average one-year return falls from **11.0% to 6.5%**: competing on relative
  performance costs everyone return.
- The result barely depends on what investors expect: any belief about the average between 1.0
  and 1.3 leads to a realised average between 1.059 and 1.070.

`Python` · `PyTorch` · `NumPy/SciPy` · finite differences · PINNs · AMS 516, Stony Brook (team of two)

## 🧭 Research Interests

- **Mean-field games & stochastic control:** HJB / Fokker–Planck solvers, physics-informed neural networks
- **Portfolio optimization:** mean-variance, Black-Litterman, hierarchical risk parity
- **Statistical arbitrage:** mean-reverting portfolios, pairs trading, meta-labeling
- **Market microstructure:** limit order books, order-flow clustering
- **Regime & changepoint detection:** Bayesian online changepoint methods

## 🛠️ Toolkit

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?logo=scipy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?logo=scikitlearn&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white)

## 📫 Contact

[LinkedIn](https://www.linkedin.com/in/deepak-s-4351102a1)

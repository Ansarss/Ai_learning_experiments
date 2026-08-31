## Microsoft Stock Price Analysis Using Stochastic Processes

This project applies stochastic-process modeling and Monte Carlo simulation to historical Microsoft Corporation (MSFT) stock prices.

The objective is to compare two stochastic models for short-term stock-price behavior:

- Geometric Brownian Motion (GBM)
- Ornstein-Uhlenbeck (OU) mean-reverting process

The analysis uses three years of historical Microsoft daily stock-price data and simulates 1,000 possible future price paths over a 60-trading-day horizon.

### Dataset

Source: Kaggle - Microsoft Stock Price History

Historical period used:

- April 20, 2023 to April 20, 2026
- 752 daily price observations
- 751 daily log-return observations

Variables include:

- Date
- Open
- High
- Low
- Close
- Volume

Daily logarithmic returns were calculated as:

`r_t = ln(S_t / S_(t-1))`

### Historical Statistics

| Metric | Value |
|---|---:|
| Starting simulation price | $418.07 |
| Mean daily log return | 0.000536 |
| Daily volatility | 0.014941 |
| Annualized log return | 13.51% |
| Annualized volatility | 23.72% |

### Geometric Brownian Motion

GBM models stock prices using a continuous stochastic process with drift and volatility:

`dS_t = μS_t dt + σS_t dW_t`

The model was calibrated using Microsoft's historical annualized return and volatility.

Simulation settings:

- 1,000 Monte Carlo simulations
- 60 trading days
- 252 trading days per year
- Random seed = 42

#### GBM Results

| Metric | Result |
|---|---:|
| Mean 60-day price | $431.70 |
| Median 60-day price | $430.83 |
| Probability of loss | 40.20% |
| 95% terminal-price interval | $346.03 - $530.22 |

GBM produced increasing dispersion as the simulation horizon expanded, illustrating how uncertainty accumulates over time.

### Ornstein-Uhlenbeck Process

The Ornstein-Uhlenbeck process introduces mean reversion:

`S_(t+1) = S_t + θ(μ - S_t) + σZ_t`

OU parameters were estimated from historical Microsoft price changes using lagged-price regression.

Estimated parameters:

| Parameter | Estimate |
|---|---:|
| Daily mean-reversion speed | 0.008259 |
| Estimated long-run price | $432.92 |
| Daily OU volatility | $6.0189 |

#### OU Results

| Metric | Result |
|---|---:|
| Mean 60-day price | $423.89 |
| Median 60-day price | $425.29 |
| Probability of loss | 43.20% |
| 95% terminal-price interval | $355.70 - $491.48 |

The OU process generated a narrower distribution because simulated prices were continuously pulled toward the estimated long-run mean.

### Model Comparison

| Metric | GBM | Ornstein-Uhlenbeck |
|---|---:|---:|
| Starting Price | $418.07 | $418.07 |
| Mean 60-Day Price | $431.70 | $423.89 |
| Median 60-Day Price | $430.83 | $425.29 |
| Probability of Loss | 40.20% | 43.20% |
| 2.5th Percentile | $346.03 | $355.70 |
| 97.5th Percentile | $530.22 | $491.48 |

GBM generated a wider range of possible future prices, while the OU model constrained extreme movements through mean reversion.

For an individual equity such as Microsoft, GBM provides the more appropriate baseline of these two models because stock prices are not generally expected to revert to a fixed historical equilibrium. The OU model is useful as a contrasting specification for understanding the effect of mean-reversion assumptions.

### Visualizations

The notebook includes:

- Historical Microsoft closing-price trend
- Daily logarithmic returns
- GBM simulated price paths
- GBM mean, median, and 95% simulation interval
- GBM terminal-price distribution
- OU simulated price paths
- OU mean, median, and 95% simulation interval
- OU terminal-price distribution
- GBM vs. OU comparison

### Technologies

- Python
- NumPy
- pandas
- Matplotlib
- KaggleHub
- Google Colab
- Monte Carlo Simulation
- Stochastic Differential Equations

### Key Takeaways

- Historical Microsoft data produced a positive estimated return but substantial volatility.
- GBM generated higher expected prices but a wider range of possible outcomes.
- OU produced more concentrated outcomes because of its mean-reverting structure.
- Both models estimated a substantial probability of loss over the 60-day horizon.
- Simulated expected prices should not be interpreted as deterministic price forecasts.
- Stochastic simulation is most useful for evaluating distributions of possible outcomes and investment risk.

### Limitations

The models rely on historical parameter estimates and simplified assumptions.

GBM assumes constant drift and volatility and does not explicitly model large market jumps or volatility clustering.

The OU process assumes a stable long-run equilibrium price, which may not be realistic for an individual stock whose fundamental value changes over time.

Future extensions could compare these models with:

- Merton Jump-Diffusion
- Heston stochastic-volatility models
- GARCH volatility models
- Rolling-window parameter estimation
- Out-of-sample backtesting

### Notebook

[`Microsoft_stock_price_analysis.ipynb`](./Microsoft_stock_price_analysis.ipynb)

> This project is intended for statistical and educational analysis and should not be interpreted as investment advice.

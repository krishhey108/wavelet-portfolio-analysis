# Wavelet ARIMA-GARCH and Long-Trend Portfolios

A multiscale financial forecasting and portfolio backtesting project that
combines discrete wavelet decomposition, ARIMA-GARCH modeling, and
mean-variance portfolio construction.

This project studies whether separating financial returns into different
frequency components can improve forecasting and portfolio allocation
relative to conventional forecasting and equal-weight approaches.

## Project overview

Financial equity returns are heteroskedastic: their volatility changes
over time, and short-term fluctuations can obscure longer-term trends.

Because financial time series contain behavior across multiple time scales,
a single-frequency model may not adequately describe the full process.
This project uses discrete wavelet transformation to decompose financial
return series into components operating at different scales.

The resulting components separate longer-term trend information from
higher-frequency variation and noise. Forecasting models are then applied
to these components to generate expected return and volatility estimates
for portfolio construction.

## Research objectives

The project has three primary objectives:

1. Decompose financial return series into multiple wavelet frequency levels.
2. Compare conventional ARIMA-GARCH forecasts with
   wavelet-ARIMA-GARCH forecasts.
3. Use forecast outputs to construct and evaluate portfolio strategies.

The central research question is:

> Can wavelet-based preprocessing improve financial forecasting and
> portfolio performance by separating long-term trends from
> high-frequency noise?

## Methodology

### 1. Return-series preprocessing

The analysis begins with equity price data, which is transformed into
log returns for modeling.

Financial returns are used for time-series analysis because they provide a
standard framework for studying changes in asset values and volatility over
time.

### 2. Discrete wavelet transformation

Discrete wavelet transformation decomposes the return series into multiple
components:

- `A4`: Approximation component representing lower-frequency,
  longer-term behavior.
- `D1`: Highest-frequency detail component.
- `D2`: Higher-frequency detail component.
- `D3`: Intermediate-frequency detail component.
- `D4`: Lower-frequency detail component.

This decomposition allows the model to analyze different time scales
separately rather than treating all fluctuations as identical.

The wavelet decomposition is used to separate persistent movements from
short-term noise and transient volatility.

### 3. ARIMA modeling

Autoregressive and moving-average terms are used to model expected returns.
The autoregressive component uses past observations, while the moving-average
component uses past forecast errors.

A general autoregressive equation can be written as:

```text
X_t = c + phi_1 X_(t-1) + ... + phi_p X_(t-p) + epsilon_t
```

A general moving-average equation can be written as:

```text
X_t = mu + epsilon_t + theta_1 epsilon_(t-1)
      + ... + theta_q epsilon_(t-q)
```

The ARIMA framework is used to estimate the conditional mean of the return
process.

### 4. GARCH volatility modeling

GARCH models the changing conditional variance of the error process. A
general GARCH-style variance equation can be written as:

```text
sigma_t^2 = omega + alpha_1 epsilon_(t-1)^2
            + ... + alpha_q epsilon_(t-q)^2
```

This allows the model to account for volatility clustering, in which periods
of high volatility tend to be followed by additional periods of high
volatility.

### 5. Wavelet-ARIMA-GARCH forecasting

The wavelet-ARIMA-GARCH approach applies forecasting models to the wavelet
components and reconstructs forecast information across multiple scales.

Compared with a standard ARIMA-GARCH specification, the wavelet-based
approach is designed to:

- Capture longer-term movements.
- Reduce the influence of high-frequency noise.
- Produce more interpretable trend forecasts.
- Model behavior that changes across time scales.

The presented results show that the standard ARIMA-GARCH forecast remains
close to zero in several periods, while the wavelet-ARIMA-GARCH forecast
captures more structured changes in the underlying trend.

## Portfolio construction

The forecasting framework is extended into a mean-variance portfolio
allocation problem.

The portfolio objective is represented by:

```text
min_w  w^T Sigma w - q R^T w
```

where:

- `w` is the vector of portfolio weights.
- `Sigma` is the covariance matrix of asset returns.
- `R` is the vector of forecast expected returns.
- `q` is a risk-aversion or return-preference parameter.
- `w^T Sigma w` represents portfolio variance.
- `R^T w` represents forecast portfolio return.

The wavelet-ARIMA-GARCH forecasts are used to estimate the inputs required
for portfolio construction.

The project evaluates several strategies, including:

- Regular mean-variance optimization.
- Raw ARIMA-GARCH mean-variance optimization.
- Wavelet-based `A4` allocation.
- Weighted `A4` covariance allocation.
- Wavelet `D2` allocation.
- Equal-weight allocation.
- Additional low-pass benchmark strategies.

## Backtesting

The strategies are evaluated using historical backtesting on five large
technology companies.

The backtest compares strategies using metrics such as:

- Cumulative portfolio growth.
- Total simple return.
- Annualized simple return.
- Annualized volatility.
- Maximum drawdown.
- Sharpe-like performance measures.

The analysis also compares wavelet-derived portfolio signals with generic
low-pass filters and conventional mean-variance approaches.

## Main observations

The project produces several preliminary observations:

- The `A4` approximation component behaves similarly to a low-pass filter
  by emphasizing lower-frequency movements.
- The wavelet-based approach preserves longer-term trend information while
  reducing the influence of high-frequency fluctuations.
- Wavelet-ARIMA-GARCH forecasts show more structured behavior than the
  standard ARIMA-GARCH mean forecast in the presented backtests.
- The `A4`-based portfolio strategy performs strongly in the displayed
  cumulative-growth comparisons.
- Portfolio construction based on low-frequency information can be useful
  for evaluating long-trend strategies.
- The current universe consists primarily of large technology companies,
  so broader industry diversification would be an important extension.

## Repository contents

```text
wavelet-portfolio-analysis/
├── README.md
├── wavelet_analysis.ipynb
└── results/
    └── wavelet_portfolio_backtest_results.pdf
```

### Main files

- `wavelet_analysis.ipynb`: Jupyter Notebook containing the analysis,
  transformations, model fitting, visualizations, and backtesting logic.
- `results/wavelet_portfolio_backtest_results.pdf`: Detailed portfolio
  backtest output and performance summaries.
- `README.md`: Project documentation and methodology overview.

## How to view the project

The notebook can be opened using:

- Jupyter Notebook.
- JupyterLab.
- Google Colab.
- Visual Studio Code with the Jupyter extension.

To run the notebook locally, install Jupyter and the required Python
packages:

```bash
pip install jupyter pandas numpy matplotlib scipy statsmodels
jupyter notebook
```

Then open:

```text
wavelet_analysis.ipynb
```

Additional packages may be required depending on the exact implementation,
including packages for wavelet transformations, volatility modeling, and
portfolio optimization.

## Results report

The detailed portfolio results are available here:

[View the portfolio backtest results](results/wavelet_portfolio_backtest_results.pdf)

The report includes strategy comparisons, cumulative-growth plots,
drawdown comparisons, Sharpe-like metrics, and model-output summaries.

## Limitations

The results should be interpreted as historical or simulated backtest
results rather than evidence of guaranteed future investment performance.

Important limitations include:

- The backtest uses a relatively small universe of five large technology
  companies.
- Transaction costs, bid-ask spreads, and market-impact costs may not be
  fully represented.
- Backtest performance can be sensitive to model specification,
  rebalancing assumptions, and parameter choices.
- The reported Sharpe-like metric should be distinguished from a formally
  validated out-of-sample Sharpe ratio.
- Further testing is needed to evaluate look-ahead bias, data-snooping bias,
  and model stability.
- Results should be validated using rolling out-of-sample periods and
  broader asset and industry coverage.

## Future extensions

Potential improvements include:

- Expanding the universe beyond technology companies.
- Adding assets from multiple industries and sectors.
- Testing additional wavelet families and decomposition levels.
- Comparing alternative forecasting models.
- Incorporating transaction costs and realistic rebalancing constraints.
- Performing rolling and walk-forward out-of-sample evaluation.
- Testing portfolio constraints such as long-only weights and position caps.
- Comparing performance across different market regimes.
- Evaluating statistical significance and robustness across datasets.

## Associated presentation

The associated project presentation is titled:

**Wavelet ARIMA-GARCH and Long-Trend Portfolios**

The presentation discusses wavelet decomposition, ARIMA-GARCH forecasting,
mean-variance portfolio construction, and portfolio backtesting results.

[View the project presentation](results/Wavelet-Project-Final-Presentation.pdf)

## Citation

If you use this project, please cite the associated presentation or paper:

```bibtex
@misc{wavelet_arima_garch_portfolios,
  title        = {Wavelet ARIMA-GARCH and Long-Trend Portfolios},
  author       = {Krishhey Thacker},
  year         = {2026},
  note         = {BQT Project Presentation}
}
```

Replace the placeholder author names and year with the correct information.

## Disclaimer

This repository is for academic and research purposes only. It does not
constitute investment advice, a recommendation to buy or sell securities,
or a guarantee of future investment performance.

## Author

Krishhey Thacker

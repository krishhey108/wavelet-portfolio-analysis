# Wavelet-Based Portfolio Analysis

This repository contains a wavelet-based multiscale analysis and
forecast-aware portfolio backtesting project.

## Project overview

The project decomposes financial time series into multiple wavelet
components and evaluates a forecast-aware portfolio strategy against an
equal-weight benchmark.

The analysis combines wavelet decomposition with forecasting and
portfolio-performance evaluation.

## Repository contents

- `notebooks/wavelet_analysis.ipynb`: Main Jupyter Notebook containing
  the analysis, methodology, code, and visualizations.
- `results/wavelet_portfolio_backtest_results.pdf`: Detailed backtest
  output and performance summaries.
- `README.md`: Project documentation.

## How to use the notebook

Open the notebook using Jupyter Notebook, JupyterLab, Google Colab, or
Visual Studio Code with the Jupyter extension.

To run it locally:

```bash
pip install jupyter pandas numpy matplotlib scipy statsmodels
jupyter notebook
```

Then open:

```text
notebooks/wavelet_analysis.ipynb
```

Additional packages may be required depending on the implementation.

## Results

The results report compares the forecast-aware wavelet strategy with an
equal-weight benchmark using return, volatility, cumulative-growth, and
Sharpe-like performance measures.

The reported figures are historical or simulated backtest results and
should not be interpreted as guaranteed future investment performance.

## Limitations

The backtest includes instances in which ARIMA-GARCH optimization failed
and observations were skipped. Results should therefore be interpreted
with care.

Further validation should examine look-ahead bias, transaction costs,
slippage, out-of-sample performance, parameter sensitivity, and the
treatment of failed model fits.

## Associated publication

The associated project or paper is available through Google Scholar:

https://colab.research.google.com/drive/1osqSShRU-XQ-mogV_R51H6QPXjzvg70l?usp=sharing 

## Author

Krishhey Thacker

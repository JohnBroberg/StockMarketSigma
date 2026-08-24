# StockMarketSigma

Standard-deviation analysis of historical S&P 500 closing values. The project uses the historical level of the S&P 500 to calculate its mean, standard deviation, and upper sigma thresholds, then visualizes the series and its distribution.

This is a descriptive analysis of index levels, not an investment strategy or a return forecast.

## Notebooks

- [`StockMarketSigma_CSV.ipynb`](StockMarketSigma_CSV.ipynb) loads the included [`SP500.csv`](SP500.csv). Use this notebook for a reproducible analysis that does not require network access or an API key.
- [`StockMarketSigma_API.ipynb`](StockMarketSigma_API.ipynb) requests the FRED `SP500` series for the previous 10 years, ending yesterday. It also calculates the current z-score and labels the current level relative to the sigma thresholds.

Both notebooks produce:

- the mean and sample standard deviation of the observations;
- `+1 sigma`, `+2 sigma`, and `+2.5 sigma` upper thresholds;
- a histogram and a kernel-density visualization; and
- a time-series chart with the mean and thresholds overlaid.

## Method

For the observed S&P 500 values $x_1, x_2, ..., x_n$, the notebooks calculate:

```text
mean = average(x)
standard deviation = pandas Series.std()
threshold(k) = mean + k * standard deviation
z-score = (current close - mean) / standard deviation
```

The `+2 sigma` and `+2.5 sigma` levels are included as reference points inspired by Jeremy Grantham's discussion of bubbles and superbubbles. They should not be interpreted as definitive market signals.

## Requirements

- Python 3
- Jupyter Notebook support, such as JupyterLab or the VS Code Jupyter extension
- `pandas`
- `numpy` (used by the CSV notebook)
- `matplotlib`
- `seaborn`
- `requests` (used by the API notebook)

Install the Python packages with:

```bash
python -m pip install jupyter pandas numpy matplotlib seaborn requests
```

## Run The CSV Analysis

1. Clone or download this repository.
2. Open `StockMarketSigma_CSV.ipynb` in Jupyter or VS Code.
3. Select a Python 3 kernel and run the cells from top to bottom.

The notebook expects `SP500.csv` in the repository root. The CSV must contain `observation_date` and `SP500` columns.

## Run The FRED Analysis

The API notebook uses the [FRED API](https://fred.stlouisfed.org/docs/api/fred/) and the FRED `SP500` series. A FRED API key is required.

1. Create a FRED API key through your FRED account.
2. Copy `.env.example` to `.env`.
3. Replace `your_fred_api_key_here` in `.env` with your key:

	```text
	FRED_API_KEY=your_fred_api_key_here
	```

4. Open `StockMarketSigma_API.ipynb` and run the cells from top to bottom.

The notebook reads `FRED_API_KEY` from the process environment first and then from the local `.env` file. `.env` is ignored by Git; do not commit your API key.

## Data Sources

- Local CSV data and the API notebook's live observations: [FRED S&P 500 series (SP500)](https://fred.stlouisfed.org/series/SP500)
- API documentation: [FRED API documentation](https://fred.stlouisfed.org/docs/api/fred/)
- Analysis context: [Jeremy Grantham, "Let the Wild Rumpus Begin"](https://www.gmo.com/globalassets/articles/viewpoints/2022/gmo_let-the-wild-rumpus-begin_1-22.pdf)

FRED data and the API response can change over time. Re-running the API notebook may therefore produce different observations and thresholds than an earlier run.

## Repository Layout

```text
StockMarketSigma/
├── SP500.csv
├── StockMarketSigma_CSV.ipynb
├── StockMarketSigma_API.ipynb
├── .env.example
├── archive/
└── LICENSE
```

## License

This project is available under the [MIT License](LICENSE).

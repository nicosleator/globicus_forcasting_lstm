# globicus-forecasting-lstm

An LSTM neural network for forecasting monthly economic time series from the
[Federal Reserve Bank of St. Louis (FRED)](https://fred.stlouisfed.org/).
To switch between series, edit only the **Configuration** cell at the top of
the notebook — all other cells run unchanged.

## Prerequisites

- Python 3
- The following packages:
  - tensorflow
  - pandas
  - numpy
  - scikit-learn
  - scipy
  - seaborn
  - matplotlib

## Data

All datasets are included in the repository, sourced from FRED.

| File | Series | Description |
|---|---|---|
| `PAYEMS.csv` | PAYEMS | Total Nonfarm Payroll Employment |
| `UNRATE.csv` | UNRATE | Unemployment Rate |

## Configuration

Edit the top cell of the notebook to switch between series:
```python
col      = "PAYEMS"         # column name in CSV
csv_file = "PAYEMS.csv"     # filename
lr       = 1e-4             # learning rate
```

| Series | CSV | LR |
|---|---|---|
| PAYEMS | PAYEMS.csv | 1e-4 |
| UNRATE | UNRATE.csv | 1e-4 |

## How It Works

1. Missing values are filled using the midpoint of surrounding observations
2. A 12-month sliding window is used to predict the following month
3. Data is scaled using MinMaxScaler fit on the training set only
4. An LSTM is trained on 80% of the data and validated on the remaining 20%
5. The model produces a 3-month forecast by feeding its own predictions back as input

## Performance

| Series | Train MSE | Train R² | Test MSE | Test R² |
|---|---|---|---|---|
| PAYEMS | 0.000424 | 0.9958 | 0.000685 | 0.9167 |
| UNRATE | 0.003861 | 0.8945 | 0.018035 | 0.7152 |

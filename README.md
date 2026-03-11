## globicus-forecasting-lstm

LSTM neural networks trained on three Federal Reserve economic series to forecast 
one month ahead and produce short-term projections.

## Prerequisites

- Python 3

## Data

The dataset "PATEMS.csv" is included in the repository as CSVs, originally sourced from 
[FRED](https://fred.stlouisfed.org/).

## How It Works

1. The last 12 months of values are used as features to predict the next month
2. Data is scaled using MinMaxScaler fit on the training set
3. An LSTM model is trained on 80% of the data and validated on the remaining 20%
4. The model forecasts 3 months into the future by feeding its own predictions back as input

## Model

| Series | Hidden Units | Batch Size | Epochs | Learning Rate |
|---|---|---|---|---|
| PAYEMS | 32 | 32 | 30 | 1e-4 |


## Performance

| Series | Train MSE | Train R² | Test MSE | Test R² |
|---|---|---|---|---|
| PAYEMS | 0.000424 | 0.9958 | 0.000685 | 0.9167 |

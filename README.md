## PAYEMS Employment Forecaster

An LSTM neural network that predicts US nonfarm payroll employment (PAYEMS) 
using data from the Federal Reserve Bank of St. Louis (FRED).

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

The model uses the PAYEMS series (Total Nonfarm Payroll Employment) from FRED. 
Download it as a CSV from https://fred.stlouisfed.org/series/PAYEMS and place 
it in the project root as `PAYEMS.csv`.

## How It Works

1. The last 12 months of employment values are used as features (L=12) to predict the next month
2. Data is scaled using MinMaxScaler fit on the training set
3. An LSTM model is trained on 80% of the data and validated on the remaining 20%
4. The model then forecasts 3 months into the future by feeding its own predictions back as input

## Model

- Architecture: LSTM (32 units) → Dense (1 unit)
- Optimizer: Adam (lr=1e-4)
- Loss: MSE
- Epochs: 30, Batch size: 32

## Performance

| Metric | Train | Test |
|---|---|---|
| MSE | 0.000424 | 0.000685 |
| R² | 0.9958 | 0.9167 |

## Output

The model prints a 3-month employment forecast in original units (thousands of persons):
```
      date          pred
2025-09-01 159817.640625
2025-10-01 159923.609375
2025-11-01 160034.671875

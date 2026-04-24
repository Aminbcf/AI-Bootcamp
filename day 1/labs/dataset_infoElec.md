# Day 3 Dataset: Electricity Consumption (Forecasting)

## Recommended Use
- Task type: Time-series forecasting
- Target example: `Consumption`

## Kaggle Link
- https://www.kaggle.com/datasets/robikscube/hourly-energy-consumption

## Public CSV Link (works without Kaggle login)
- https://raw.githubusercontent.com/jenfly/opsd/master/opsd_germany_daily.csv

## Loader Cell (Kaggle + Local)
```python
import os
import urllib.request
import pandas as pd

IS_KAGGLE = os.path.exists('/kaggle/working')

if IS_KAGGLE:
    # Add this dataset in Kaggle first:
    # https://www.kaggle.com/datasets/robikscube/hourly-energy-consumption
    kaggle_candidates = [
        '/kaggle/input/hourly-energy-consumption/PJME_hourly.csv',
        '/kaggle/input/hourly-energy-consumption/AEP_hourly.csv',
        '/kaggle/input/hourly-energy-consumption/COMED_hourly.csv',
    ]

    path = None
    for p in kaggle_candidates:
        if os.path.exists(p):
            path = p
            break

    if path is not None:
        df = pd.read_csv(path)
        df.columns = ['Datetime', 'Consumption']
    else:
        # Fallback to OPSD daily dataset if Kaggle files are not found
        path = 'opsd_germany_daily.csv'
        if not os.path.exists(path):
            urllib.request.urlretrieve(
                'https://raw.githubusercontent.com/jenfly/opsd/master/opsd_germany_daily.csv',
                path
            )
        df = pd.read_csv(path)
        df = df[['Date', 'Consumption']].dropna().copy()
        df.columns = ['Datetime', 'Consumption']
else:
    path = 'opsd_germany_daily.csv'
    if not os.path.exists(path):
        urllib.request.urlretrieve(
            'https://raw.githubusercontent.com/jenfly/opsd/master/opsd_germany_daily.csv',
            path
        )
    df = pd.read_csv(path)
    df = df[['Date', 'Consumption']].dropna().copy()
    df.columns = ['Datetime', 'Consumption']

print('Loaded source:', path)
print(df.shape)
df.head()
```

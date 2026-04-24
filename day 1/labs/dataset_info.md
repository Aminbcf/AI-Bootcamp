# Day 2 Dataset: Palmer Penguins

## Recommended Use
- Task type: Classification
- Target example: `species`

## Kaggle Link
- https://www.kaggle.com/datasets/parulpandey/palmer-archipelago-antarctica-penguin-data

## Public CSV Link (works without Kaggle login)
- https://raw.githubusercontent.com/mwaskom/seaborn-data/master/penguins.csv

## Loader Cell (Kaggle + Local)
```python
import os
import urllib.request
import pandas as pd

IS_KAGGLE = os.path.exists('/kaggle/working')

if IS_KAGGLE:
    # Add this dataset in Kaggle first:
    # https://www.kaggle.com/datasets/parulpandey/palmer-archipelago-antarctica-penguin-data
    kaggle_candidates = [
        '/kaggle/input/palmer-archipelago-antarctica-penguin-data/penguins_size.csv',
        '/kaggle/input/palmer-archipelago-antarctica-penguin-data/penguins_lter.csv',
    ]

    path = None
    for p in kaggle_candidates:
        if os.path.exists(p):
            path = p
            break

    if path is None:
        raise FileNotFoundError('Penguins file not found in Kaggle input folder.')
else:
    path = 'penguins.csv'
    if not os.path.exists(path):
        urllib.request.urlretrieve(
            'https://raw.githubusercontent.com/mwaskom/seaborn-data/master/penguins.csv',
            path
        )

df = pd.read_csv(path)
print('Loaded from:', path)
print(df.shape)
df.head()
```

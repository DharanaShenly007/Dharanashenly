# Dharanashenly
Nanmudalvan project 

pip install jovian opendatasets --upgrade --quiet
output
 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
68.6/68.6 kB 1.4 MB/s eta 0:00:00
 Preparing metadata (setup.py) ... done
 Building wheel for uuid (setup.py) ... done
[2]
0s
# Downloading Data from Kaggle
dataset_url = 'https://www.kaggle.com/kianwee/agricultural-raw-material-prices￾19902020?select=agricultural_raw_material.csv'
[3]
1m
# We need to enter our API generated credentials upon prompt.
import opendatasets as od
od.download(dataset_url)
output
Please provide your Kaggle credentials to download this dataset. Learn more: http://bit.ly/kaggle-creds
Your Kaggle username: danala26
Your Kaggle Key: ··········
Downloading agricultural-raw-material-prices-19902020.zip to ./agricultural-raw-material-prices￾19902020
100%|██████████| 22.8k/22.8k [00:00<00:00, 9.90MB/s]
[4]
0s
# Importing csv file
data_dir = './agricultural-raw-material-prices-19902020'
[5]
0s
import os
os.listdir(data_dir)
output
['agricultural_raw_material.csv']
[7]
0s
project_name = "analysis-agriculture-raw-mateial￾prices" # Give project a name and use lowercase letters and hyphens only
[8]
6s
!pip install jovian --upgrade -q
9]
0s
import jovian
[10]
0s
jovian.commit(project=project_name)
output
[jovian] Detected Colab notebook...
[jovian] jovian.commit() is no longer required on Google Colab. If you ran this notebook from Jovian, 
then just save this file in Colab using Ctrl+S/Cmd+S and it will be updated on Jovian. 
Also, you can also delete this cell, it's no longer necessary.
[11]
2s
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.impute import SimpleImputer
sns.set(rc={'figure.figsize':(11, 4)})
# reading the csv data
agri_price_df = pd.read_csv('./agricultural-raw-material-prices￾19902020/agricultural_raw_material.csv')
[12]
0s
# columns list
agri_price_df.info()
output
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 361 entries, 0 to 360
Data columns (total 25 columns):
# Column Non-Null Count Dtype 
--- ------ -------------- ----- 
0 Month 361 non-null object 
1 Coarse wool Price 327 non-null object 
2 Coarse wool price % Change 327 non-null object 
3 Copra Price 339 non-null object 
4 Copra price % Change 339 non-null object 
5 Cotton Price 361 non-null float64
6 Cotton price % Change 361 non-null object 
7 Fine wool Price 327 non-null object 
8 Fine wool price % Change 327 non-null object 
9 Hard log Price 361 non-null float64
10 Hard log price % Change 361 non-null object 
11 Hard sawnwood Price 327 non-null float64
12 Hard sawnwood price % Change 327 non-null object 
13 Hide Price 327 non-null float64
16 Plywood price % Change 361 non-null object 
17 Rubber Price 361 non-null float64
18 Rubber price % Change 361 non-null object 
19 Softlog Price 327 non-null float64
20 Softlog price % Change 327 non-null object 

21 Soft sawnwood Price 327 non-null float64

22 Soft sawnwood price % Change 327 non-null object 

23 Wood pulp Price 360 non-null float64

24 Wood pulp price % Change 360 non-null object 

dtypes: float64(9), object(16)

memory usage: 70.6+ KB

[13]

0s

# It is advisable to make a copy of your dataset, so that we can return to the original data in case we mad

e some wrong computation in our data.

agri_price_df_copy = agri_price_df.copy()

[14]

0s

# Replacing %, "," and "-"

agri_price_df = agri_price_df.replace('%', '', regex=True)

agri_price_df = agri_price_df.replace(',', '', regex=True)

agri_price_df = agri_price_df.replace('-', '', regex=True)

agri_price_df = agri_price_df.replace('', np.nan)

agri_price_df = agri_price_df.replace('MAY90', np.nan)

[15]

1s

# Dropping rows with NaN values

agri_price_df = agri_price_df.dropna()

[16]

0s

# Check to see if all NaN values are resolved

agri_price_df.isnull().sum()

output

Month 0

Coarse wool Price 0

Coarse wool price % Change 0

Copra Price 0

Copra price % Change 0

Cotton Price 0

Cotton price % Change 0

Fine wool Price 0

Fine wool price % Change 0

Hard log Price 0

Hard log price % Change 0

Hard sawnwood Price 0

Hard sawnwood price % Change 0

Hide Price 0

Hide price % change 0

Plywood Price 0

Plywood price % Change 0

Rubber Price 0

Rubber price % Change 0

Softlog Price 0

Softlog price % Change 0

Soft sawnwood Price 0

Soft sawnwood price % Change 0


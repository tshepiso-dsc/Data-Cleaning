import pandas as pd

#LOAD CSV FILE
df = pd.read_csv('financial_fraud_detection_dataset.csv')
df.head()

#PRINTING COLUMN NAMES
print("Colunm Names")
print(df.columns.tolist())

#PRINT INFO
df.info()

#IDENIFY NULL VALUES
df.isnull().sum()

#DROP NULL VALUES
df['fraud_type'] = df['fraud_type'].fillna('None')
df['time_since_last_transaction'] = df['time_since_last_transaction'].fillna(0)


#Identify Duplicates
df.duplicated().count()

#Remove Duplicates
df.drop_duplicates()
  print(len(df))

#Print Data Types
print(df.dtypes)

#Change Data Types
df['timestamp'] = pd.to_datetime(df['timestamp'], format='mixed', errors='coerce')
categorial_col = ['transaction_type', 'merchant_category', 'device_used', 'fraud_type', 'payment_channel']
  for col in categorial_col:
        df[col] = df[col].astype('category')       
df['is_fraud'] = df['is_fraud'].astype(int)


#Print New data Types
print(df.dtypes)

#Drop NA
df['timestamp'].isna()

#Import Stats Libraries
import numpy as np
from scipy.stats import zscore
import matplotlib.pyplot as plt

#Outlier Detection 
Q1 = df['amount'].quantile(0.25)
Q3 = df['amount'].quantile(0.75)
IQR = Q3 - Q1
outliers = df[(df['amount'] < Q1 - 1.5 * IQR) | (df['amount'] > Q3 + 1.5 * IQR)]
print(outliers)

#Inport Visualisation Libraries
import seaborn as sns
import matplotlib.pyplot as plt
  sns.boxplot(x=df['amount'])
  plt.show()

#Cutting Outliers
lower = df['amount'].quantile(0.05)
upper = df['amount'].quantile(0.95)
df['amount'] = df['amount'].clip(lower, upper)


#Split date-time into separate columns
df['hour'] = df['timestamp'].dt.hour
df['day'] = df['timestamp'].dt.day
df['month'] = df['timestamp'].dt.month
df['year'] = df['timestamp'].dt.year
df['weekday'] = df['timestamp'].dt.weekday


#export cleaned data to csv
df.to_csv('clean_fraud_data.csv')



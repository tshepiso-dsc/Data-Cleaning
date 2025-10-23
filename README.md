Step 1: Data Cleaning
1.	Load the Data
   •	Use pandas to load the dataset.
   •	Check for memory efficiency (consider using dtypes optimization).
3.	Handle Missing Values
   •	Identify missing values using .isnull().sum().
   •	Decide on imputation strategies:
      o	Numerical: mean/median or predictive imputation.
      o	Categorical: mode or "Unknown".
      o	Drop rows/columns if missingness is too high.
5.	Remove Duplicates   
   •	Check for duplicate transaction_ids or rows.
7.	Convert Data Types   
   •	Ensure timestamp is in datetime format.
   •	Convert categorical columns to category dtype for memory efficiency.
9.	Outlier Detection (clip or remove)    
   •	Use boxplots or z-scores for columns like amount, velocity_score, etc.
   •	Consider log transformation for skewed distributions.
11.	Feature Engineering    
   •	Extract time-based features from timestamp (hour, day, weekday, etc.).
   •	Encode categorical variables (transaction_type, merchant_category, etc.) using:
      o	One-hot encoding (for tree-based models).
      o	Label encoding or embeddings (for neural networks).


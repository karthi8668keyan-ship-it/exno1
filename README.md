# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
Import Required Libraries from Python Library:
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt
```
Reading the file and display first five data:
```
df=pd.read_csv("Data_set.csv")
df.head()
```
Data set Information:
```
df.info()
df.describe()
```
Handling Missing values and check Null Values:
```
df.isnull()
df.isnull().sum()
```
Filling the Missing Values with 0
```
df1=df.fillna(0)
df1
```
Forward Fill using ffill()
```
df_ffill=df.ffill()
df_ffill
```
Backward fill using bfill()
```
df_bfill=df.bfill()
df_bfill
```
Filling the missing values with mean values:
```
df['rating']=df['rating'].fillna(df['rating'].mean())
df['watchers']=df['watchers'].fillna(df['watchers'].mean())
df
```
Deleting the rows which contains atleast one missing values:
```
df_dropna=df.dropna()
df_dropna
```
Save the cleaned data in new file:
```
df_dropna.to_csv('exp1 data set.csv',index=False)
```
Detecting the outliers for Data_set.csv file: Using IQR method:
```
sns.boxplot(x=df['watchers'])
plt.show()
```
Calculate Q1 and Q3 to perform Q3-Q1
```
Q1=df['watchers'].quantile(0.25)
Q3=df['watchers'].quantile(0.75)
IQR=Q3-Q1
print(f"The IQR value is {IQR}")
```
Detecting outliers:
```
outliers=df[(df['watchers']<(Q1-1.5*IQR)) | (df['watchers']>(Q3+1.5*IQR))]
outliers
```
Removing Outliers
```
removed_outliers=df[~((df['watchers']<(Q1-1.5*IQR)) | (df['watchers']>(Q3+1.5*IQR)))]
removed_outliers
```
Calculate Outliers using Z Score Method using current_overall_rank Column
```
z_score=np.abs(stats.zscore(df['rating'].dropna()))
z_score
```
Detecting Outliers
```
threshold=3
mask = np.zeros(len(df), dtype=bool)
mask[df['rating'].dropna().index] = z_score > threshold
outliers = df[mask]
print('outliers')
print(outliers)
```
Removing Outliers
```
mask = np.ones(len(df), dtype=bool) 
mask[df['rating'].dropna().index] = z_score <= threshold 
df_cleaned = df[mask]
df_cleaned
```
# Output

<img width="1093" height="715" alt="image" src="https://github.com/user-attachments/assets/2c4bc748-3762-4e7a-89c0-30d0fe2fe7a5" />

<img width="1057" height="687" alt="image" src="https://github.com/user-attachments/assets/7d246576-80bf-46f8-8b50-9cf387305093" />

<img width="1057" height="687" alt="image" src="https://github.com/user-attachments/assets/3d5dcf45-6480-45ac-8fd4-46fb3b27934f" />

<img width="1521" height="398" alt="image" src="https://github.com/user-attachments/assets/79aa25c2-5562-4faa-97c7-e47bbfee228d" />

<img width="1533" height="689" alt="image" src="https://github.com/user-attachments/assets/ce79a743-a7c2-4ff7-b918-ce059f5794b4" />

# Result
          <<include your Result here>>

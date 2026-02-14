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

# Coding

Import Required Libraries from Python Library:
```python
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt
```
Reading the file and display first five data:
```python
df=pd.read_csv("Data_set.csv")
df.head()
```
Data set Information:
```python
df.info()
df.describe()
```
Handling Missing values and check Null Values
```python
df.isnull()
df.isnull().sum()
```
Filling the Missing Values with 0
```python
df1=df.fillna(0)
df.fillna
```
Forward Fill using ffill()
```python
df_ffill=df.ffill()
df_ffill
```
Backward fill using bfill()
```python
df_bfill=df.bfill()
df_bfill
```
Filling the missing values with mean values:
```python
df['rating']=df['rating'].fillna(df['rating'].mean())
df['watchers']=df['watchers'].fillna(df['watchers'].mean())
df
```
Deleting the rows which contains atleast one missing values:
```python
df_dropna=df.dropna()
df_dropna
```
Save the cleaned data in new file:
```python
df_dropna.to_csv('exp 1 data set.csv',index=False)
```
Detecting the outliers for Data_set.csv file

Using IQR method:
```python
df=pd.read_csv('Data_set.csv')
```
Using Box Plot for Detecting Outliers:
```python
sns.boxplot(x=df['watchers'])
plt.show()
```
Calculate Q1 and Q3 to perform Q3-Q1
```python
Q1=df['watchers'].quantile(0.25)
Q3=df['watchers'].quantile(0.75)
IQR=Q3-Q1
print("The IQR value is",IQR)
```
Detecting outliers:
```python
outliers=df[(df['watchers']<(Q1-1.5*IQR)) | 
(df['watchers']>(Q3+1.5*IQR))]
outlires
```
Removing Outliers
```python
removed_outliers=df[~((df['watchers']<(Q1-1.5*IQR)) | 
(df['watchers']>(Q3+1.5*IQR)))]
removed_outliers
```
Calculate Outliers using Z Score Method using current_overall_rank Column
```python
z_score=np.abs(stats.zscore(df['rating'].dropna()))
z_score
```
Detecting Outliers
```python
threshold=3
mask = np.zeros(len(df), dtype=bool)
mask[df['rating'].dropna().index] = z_score > threshold
outliers = df[mask]
print('outliers')
print(outliers)
```
Removing Outliers
```python
mask = np.ones(len(df), dtype=bool) 
mask[df['rating'].dropna().index] = z_score <= threshold 
df_cleaned = df[mask]
df_cleaned
```
# Output

<img width="962" height="789" alt="Screenshot 2026-02-14 142239" src="https://github.com/user-attachments/assets/ebab8f19-1795-4b57-b976-512ec1fa4f79" />


<img width="1383" height="633" alt="Screenshot 2026-02-14 142324" src="https://github.com/user-attachments/assets/95fef7b4-9966-48ea-8ae1-b1698eec21ee" />


<img width="1581" height="702" alt="Screenshot 2026-02-14 142359" src="https://github.com/user-attachments/assets/3289bd9d-d001-4b53-a8f9-ee20e0b565c1" />


<img width="745" height="648" alt="Screenshot 2026-02-14 142431" src="https://github.com/user-attachments/assets/f245ece5-6622-4fad-a41f-92e342504ecb" />


<img width="1400" height="442" alt="Screenshot 2026-02-14 142454" src="https://github.com/user-attachments/assets/835610ae-57c8-4186-8aa3-6d6de975b4a8" />


<img width="1545" height="721" alt="Screenshot 2026-02-14 142516" src="https://github.com/user-attachments/assets/f648fcf2-73da-4305-ac44-acf8f33946ec" />


# Result
Thus the Data cleaning process is completed successfully

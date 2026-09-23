# Practice Problem Numpy and Pandas
This Python code creates a random dataset using NumPy and Pandas, then performs various mathematical operations, filters, and handles missing values.

---
## Importing Libraries
```python
import numpy as np
import pandas as pd
```
- NumPy(`np`): Helps with math operations (random numbers, arrays, etc.).
- Pandas(`pd`): Helps organize data into tables (DataFrames).
---
## Creating Random Data
```python
np.random.seed(55)
```
- This makes sure the random numbers are the same every time you run the code (like locking the dice roll).
```python
data = {
    "ID": np.arange(1,11),   # IDs from 1 to 10
    "Category": np.random.choice(['A','B','C'], size=10), # Random letters
    "Value1": np.random.randint(10,100, size=10), # Random integers (10–99)
    "Value2": np.random.uniform(1.0,50.0, size=10) # Random decimals (1–50)
}
df = pd.DataFrame(data)
```
- Creates a table with 10 rows and 4 columns: ID, Category, Value1, Value2.
- Example: ID=1, Category=B, Value1=45, Value2=45.03.
---
## Adding Math Operations
```python
df['Sum'] = np.add(df['Value1'], df['Value2'])
df['Difference'] = np.subtract(df['Value1'], df['Value2'])
df['Product'] = np.multiply(df['Value1'], df['Value2'])
df['Quotient'] = np.divide(df['Value1'], df['Value2'])
df['Floor_div'] = np.floor_divide(df['Value1'], df['Value2'])
df['Mod'] = np.remainder(df['Value1'], 2)
df['V1 ** 2'] = np.power(df['Value1'], 2)
df['SquareRoot_V1'] = np.sqrt(df['Value1'])
df['mean_V1'] = np.mean(df['Value1'])
df['Std_V2'] = np.std(df['Value2'])
```
- Sum(`np.add(a,b)`) → adds Value1 + Value2
- Difference(`np.subtract(a,b)`) → subtracts Value2 from Value1
- Product(`np.multiply(a,b)`) → multiplies Value1 × Value2
- Quotient(`np.divide(a,b)`) → divides Value1 ÷ Value2
- Floor_div(`np.floor_divide(a,b)`) → division but rounded down to whole number
- Mod(`np.remainder(a,b)`) → remainder when Value1 is divided by 2 (checks if even/odd)
- V1 ** 2(`np.power(a,b)`) → squares Value1
- SquareRoot_V1(`np.sqrt(a,b)`) → square root of Value1
- mean_V1(`np.mean(a,b)`) → average of all Value1 values (same for every row)
- Std_V2(`np.std(a,b)`) → standard deviation of Value2 (spread of numbers, same for every row)

#### Note:
- Some columns (like mean and std) repeat because they are overall statistics.
---
## Filtering Data
```python
filtered_df = df[(df['Value1'] > 50) & (df['Category'] == 'B')]
```
- Keeps only rows where: Value1 > 50 and Category = B.
---
## Grouping and Aggregating
```python
grouped = df.groupby('Category').agg({
    'Value1': ['mean','max','min'],
    'Value2': ['mean','sum']
})
```
- Groups rows by Category (A, B, C).
- Shows: Average, max, min of Value1 & Average and total sum of Value2.
- This is like summarizing data per group.
---
## Normalizing Values
```python
df["Value1_Normalized"] = df["Value1"].apply(lambda x: (x - np.min(df["Value1"])))
```
- Normalization rescales numbers between 0 and 1.
- Formula: `(x - min)/(max - min)`
```python
df["Value1_Normalized"] = (df["Value1"] - df["Value1"].min()) / (df["Value1"].max() - df["Value1"].min())
```
- Another way to normalize a value.
---
## Handling Missing Values
```python
df.loc[2, 'Value1'] = np.nan
df.loc[5, 'Value2'] = np.nan
```
- Replaces some values with NaN (Not a Number).
- This simulates missing data, which is common in real datasets.
- Example: Row 3 has Value1 = NaN, Row 6 has Value2 = NaN.


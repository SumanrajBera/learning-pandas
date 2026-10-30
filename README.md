# Pandas

- Pandas is a powerful tool for data manipulation and analysis.
- It has two main data structures:
  - Series(1D)
  - DataFrame(2D)
- Working with tabular data easy and fast
- Ideal for cleaning, transforming and analyzing datasets.
- Works well with other libraries like Numpy, Matplotlib and Scikit-Learn

# Creating series and dataframe

## Series
```py
import pandas as pd

a = [1,2,3,4,5]
s = pd.Series(a, name="Ranks")

# Output
# 0 1
# 1 2
# 2 3
# 3 4
# 4 5
```

## DataFrame
```py
import pandas as pd

data = {
    "Name": ["Anu", "Kanan", "Amit"],
    "Marks": [50, 40, 60],
    "Subject": ["Maths","Science", "History"]
}

df = pd.DataFrame(data)
```
**Output:**
|     | Name  | Marks | Subject |
| --- | ----- | ----- | ------- |
| 0   | Anu   | 50    | Maths   |
| 1   | Kanan | 40    | Science |
| 2   | Amit  | 60    | History |
- We can pass extra parameters such as `columns = []` in the square bracket we can mention names to name a 2D array columns or for selecting which columns to be shown if already named.

### Inspecting Data
- head(n) → first n rows (default is 5 rows from start)
- tail(n) → last n rows (default is 5 rows from end)
- info() → columns, non-null counts, and dtypes
- shape → (rows, columns)
- dtypes → data type of each column

### Selecting rows and columns
- Single column → df['col']
- Multiple columns → df[['col1','col2']]
- Label-based selection → df.loc[row_label, col_label]
- Integer-index selection → df.iloc[row_idx, col_idx] 

*Note* We can also mention a range in loc and iloc using `:`

### Get Overview
- df.index → row labels
- df.columns → column names
- df.values → underlying NumPy array (read-only; prefer using DataFrame ops)

### Renaming columns and setting index
- Rename columns → df.rename(columns={'old':'new'}, inplace=False)
- Set a column as index → df.set_index('column_name', inplace=False)
- Reset index → df.reset_index(inplace=False) If you don't use inplace=True, remember to assign the result back to a variable.
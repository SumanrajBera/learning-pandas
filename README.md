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
  
## Data Cleaning and Preparation

### Handling Missing Data
- **isna()** / **isnull()** → detect missing values (returns True/False)
```py
# To sum how many null values are present column-wise
dataFrame.isna().sum()

# Here, axis = 0 means for column-wise "travel vertically down the rows."
# axis = 1 means for row-wise "travel horizontally across the columns."
```
- **dropna()** → remove missing values (rows/columns)
- **fillna()** → replace missing values with a given value or method (e.g., forward fill)

### Changing datatype

We can make use of `astype()` to change a column's datatype to our desired datatype
```py
df['Column_Name'] = df['Column_Name'].astype(datatype)
```

### Replacing values

We can use `replace()` to substitute specific values or patterns.
```py
# For single values
c['Name'] = c['Name'].replace("Bob", "Robert")

# For multiple value
c['Age'] = c['Age'].replace({25:20, 35:40})
```

### Dropping value by row or column
- drop(labels or index, axis=0) → drop rows by index or labels.
```py
# Row with index 1 remove
print(df.drop(1))
# Drop multiple row by index value
print(df.drop([0,1]))
```
- drop(labels, axis=1) → drop columns by name.
```py
# Age column remove
df = df.drop("Age", axis=1)
```
- Use `inplace=True` if you want to modify the DataFrame directly.

### Detecting & Removing Duplicates
- `duplicated()` → returns a Boolean Series marking duplicate rows.
- `drop_duplicates()` → remove duplicate rows.
```py
# Normally deletes only duplicate values only
print(df.drop_duplicates())

# In the subset we can give column names or labels for dropping duplicates based on that
print(df.drop_duplicates(subset=["Age"]))

# For deleting all except first occurencnce use "first" 
# For deleting all except last occurencnce use "last" 
# For deleting all duplicated values along with original use "False" 
print(df.drop_duplicates(keep="last"))
```

## Data selection & Filtering

### Boolean Indexing & Conditional Selection
- Use comparison operators to build conditions (e.g., df['col'] > 50).
- Pass the condition inside df[...] to get matching rows.
```py
print(df["Age"] > 30) # Will give the column with boolean values
# To get the rows of data
df[df["Age"] > 30]
```
- Combine multiple conditions with & (AND), | (OR), and ~ (NOT).
- Parentheses are required when combining conditions.
```py
# We can combine condition using logical operators &, | and ~
# Paranthesis is a must for combining logical operators
df[(df["Age"] > 30) & (df["City"] == "Mumbai")]
```
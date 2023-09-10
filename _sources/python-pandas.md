---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Pandas

Pandas is a powerful Python library for data manipulation and analysis. It provides data structures and functions to efficiently work with structured data, such as tabular data and time series. Pandas introduces two primary data structures, namely Series and DataFrame, which allow for easy indexing, slicing, filtering, and transformation of data. With Pandas, you can handle missing data, perform statistical calculations, apply data reshaping operations, and visualize data. It also integrates well with other libraries, such as NumPy and Matplotlib, making it a popular choice for data analysis tasks, data cleaning, preprocessing, and exploratory data analysis (EDA).

```{code-cell}
import pandas as pd
```

## Series

### Creation

```{code-cell}
sr = pd.Series(data = [10, 20, 30], name = 'sum_10')  # simple creation with name
sr
```

```{code-cell}
sr2 = pd.Series(data = [10, 20, 30],  # creation with indexes
          index = ['a', 'b', 'c'])
sr2
```

```{code-cell}      
sr3 = pd.Series(data = {'a': 10, 'b': 20, 'c': 30})  # creation from dictionary
sr3
```

`name`: returns the name of the series\
`rename`: changes the name\
`dtype`: returns the type of the elements in the series\
`index`: returns the indexes of the series\
`to_numpy`: access data underlying the array

```{code-cell}
print(sr.name)
print(sr.rename('sum'))
print(sr.dtype)
print(sr.index)
print(sr.to_numpy())
```

### Access, Operations, Functions

Just as Numpy's arrays


### Series of Strings Methods

| Method | Paramethers | Description |
| :----: | :---------: | :---------: |
| `str.cat`         | others=None, sep=None | Concatenates strings in the series with given separator |
| `str.split`       | pat*=None, n=-1       | Splits strings in the series around given separator from the beginning |
| `str.rsplit`      | pat*=None, n=-1       | Splits strings in the series around given separator from the end |
| `str.get`         | i                     | Extracts element from each component at specified position in the series |
| `str.join`        | sep                   | Joins lists contained as elements in the series with passed delimiter |
| `str.get_dummies` | sep*='|'              | Splits strings on the separator returning dataframe of dummy variables |
| `str.contains`    | pat, regex*=True      | Returns boolean series if each string contains pattern/regex |
| `str.replace`     | pat, repl, n=-1, regex*=True | Replaces occurrences of pattern/regex with some other string or the return value of a callable given the occurrence |

Others as python-basics: `str.capitalize`, `str.casefold`, `str.lower`, `str.upper`, `str.len`, ...


## Dataframe

### Creation

```{code-cell}
df = pd.DataFrame([[1, 2, 3],  # simple dataframe creation (from lists)
              [4, 5, 6],
              [7, 8, 9]])
```

```{code-cell}
df = pd.DataFrame([[1, 2, 3],  # creation with indexes and colunms names
              [4, 5, 6],
              [7, 8, 9]],
             index = ['R1', 'R2', 'R3'],
             columns = ['C1', 'C2', 'C3'])
```

**Creation from a Support**

| Support | Example |
| :-----: | :-----: |
| Array | `pd.DataFrame(np.array([['Tom', 7], ['Mike', 15], ['Tiffany', 3]]))` |
| Dictionary | `pd.DataFrame({'Name': ['Tom', 'Mike', 'Tiffany'], 'Number': [7, 15, 3]})` |
| List | `pd.DataFrame([['Tom', 7], ['Mike', 15], ['Tiffany', 3]])` |
| List of Dictionaries | `pd.DataFrame({'Name': 'Tom', 'Number': 7}, {'Name': 'Mike', 'Number': 15}, {'Name': 'Tiffany', 'Number': 3}` |
| Series | `pd.DataFrame({'Name': pd.Series(['Tom', 'Mike', 'Tiffany']), 'Number': pd.Series([7, 15, 3])})` |
| Tuple | `pd.DataFrame(zip(['Tom', 'Mike', 'Tiffany'], [7, 15, 3]))` |

**Creation from File**

| File | Function |
| :--: | :------: |
| CSV | `read_csv` |
| Excel | `read_excel` |
| Html | `read_html` |
| Json | `read_json` |
| Text | `read_csv` with `delimiter='\t'` |

### Access

1) Indexing with `[]`

```{code-cell}
df['C1']  # returns a series from a column
```

```{code-cell}
df[['C1']]  # returns a dataframe from a column

# df[0:1]  returns a dataframe from a row
```

```{code-cell}
df[['C1', 'C2']]  # returns a dataframe with multiple columns

# df[0:2]  returns a dataframe with multiple rows
```

2) Boolean indexing

Boolean indexing in Pandas is a technique where you filter rows from a DataFrame by using a series of boolean values. Each boolean value indicates whether a specific condition is met for its corresponding row. By applying this boolean series as an index to the DataFrame, you retrieve only the rows that fulfill the condition. It's a convenient method for extracting subsets of data that adhere to specific logical requirements.

```{code-cell}
df[df['C1'] > 1]
```
It returns an Object for single selection, Series for one row/column, otherwise DataFrame

3) `loc` method

Using the `loc` function in Pandas involves selecting data from a DataFrame based on label-based indexing. You specify row and column labels to access specific data points. This method is particularly useful when you want to work with data using its meaningful labels rather than numeric positions. It provides a convenient way to extract data based on labels, enhancing readability and understanding.
```{code-cell}
df.loc[['R1', 'R2'], ['C1']]
```
It returns an Object for single selection, Series for one row/column, otherwise DataFrame

4) `iloc` method

Using `iloc` in Pandas means selecting data from a DataFrame by specifying integer-based row and column indices. This approach lets you retrieve data using numerical positions, offering a precise way to extract information from specific locations within the DataFrame. It's particularly useful for numeric-oriented data retrieval tasks.

```{code-cell}
df.iloc[[0, 1], [0]]
```
It returns an Object for single selection, Series for one row/column, otherwise DataFrame

5) `query` method

The `query` function in Pandas allows you to filter a DataFrame by providing a string expression that represents a condition. This expression is evaluated to produce a boolean series that identifies rows matching the condition. This function simplifies the process of filtering data based on specific criteria, making the code more concise and readable. It's a helpful tool for selecting rows that meet certain conditions in a more intuitive and SQL-like manner.
```{code-cell}
df.query('C1 > 1 & C2 == 5')
```
It returns an Object for single selection, Series for one row/column, otherwise DataFrame

### Inspection

```{code-cell}
df = pd.read_csv('cycling_data.csv')
```

`head`: returns the firsts n rows (default = 5) of the dataframe\
`tail`: returns the lasts n rows (default = 5) of the dataframe\
`shape`: returns the shape of the dataframe\
`dtypes`: returns the type of the elements in the dataframe\
`info`: returns information about the dataframe itself, such as dtypes, memory usages and non-null values\
`describe`: provides summary statistics of the values within a dataframe

Examples:

```{code-cell}
df.head(10)  # shows the firsts 10 rows
```

```{code-cell}
df.tail(10)  # shows the lasts 10 rows
```

```{code-cell}
df.shape  # shape[0] are rows, shape[1] are columns
```

```{code-cell}
df.dtypes
```

```{code-cell}
df.info()
```

```{code-cell}
df.describe()

# df.describe(include='all')  include all the summaries
```

### View vs Copy

A **view** of a DataFrame is a representation that provides access to a subset of the original data. Changes made to the view will affect the original DataFrame, as they both share the same underlying data.

A **copy** of a DataFrame is an independent duplicate with identical data to the original at the time of copying. Modifications to a copy do not impact the original DataFrame, and vice versa.

```{code-cell}
df_copy = df.copy()
```

It is important to note that accessing the dataframe via [], Boolean indexing, or query generates a copy of the original dataframe, whereas the loc and iloc functions use a view. Consequently, it is necessary to use these two functions to modify values within the original dataset.

### Operations

**Rename**

```{code-cell}
df = df.rename(columns={'Date': 'Datetime', 'Comments': 'Notes'})  # rename columns
# df.rename(columns={'Date': 'Datetime', 'Comments': 'Notes'}, inplace=True)  equivalent

df.head()
```

```{code-cell}
df = df.rename(index={0: 'row_1', 2: 'row_3'})  # rename rows
# df.rename(index={0: 'row_1', 2: 'row_3'}, inplace=True)  equivalent

df.head()
```

```{code-cell}
df = df.set_index('Datetime')
df.head()
```

```{code-cell}
df = df.reset_index()
df.head()
```

**Add** and **Remove**

This section only considers cases where only one row/column is to be added or deleted. The results can be easily generalized to the case of multiple rows or columns (see also the next section), for example, using Dataframes instead of Series.

1) Add Column
```{code-cell}
df['Avg Speed'] = df['Distance'] * 1000 / df['Time']  # direct method (using series)
# df['Avg Speed'] = pd.Series([6, 5, 6, ...])  example with explicit series

# Alternatives
# 1) df.loc[:, 'Avg Speed'] = df['Distance'] * 1000 / df['Time']  # loc
# 2) df.iloc[:, df.shape[1]] = df['Distance'] * 1000 / df['Time']  #iloc
#    df.columns = [*df.columns[:-1], 'Avg Speed']

df.head()
```

2) Remove Column
```{code-cell}
df = df.drop(columns=['Avg Speed'])
df.head()
```

3) Add Row
```{code-cell}
new_row = pd.Series(['12 Oct 2019, 00:10:57', 'Morning Ride', 'Ride',
                    2331, 12.67, 'Washed and oiled bike last night'],
                    index = df.columns)
df.loc[df.index.max() + 1] = new_row

# Alternative
# df.iloc[df.shape[0]] = new_row

df.tail()
```

4) Remove Row
```{code-cell}
df = df.drop(index=[30, 31, 32, 33])
# df = df.drop(index=df.index[30:])  equivalent

df.tail()
```

**Reshape**

1) Pivot

![](reshaping_pivot.png)

```{code-cell}
df = pd.DataFrame({'foo': ['one', 'one', 'one', 'two', 'two', 'two'],
                    'bar': ['A', 'B', 'C', 'A', 'B', 'C'],
                    'baz': [1, 2, 3, 4, 5, 6],
                    'zoo': ['x', 'y', 'z', 'q', 'w', 't']})
df.pivot(index = 'foo', columns = 'bar', values = 'baz')
```

2) Stack

![](reshaping_stack.png)

```{code-cell}
index_tuples = [('bar', 'one'), ('bar', 'two'), ('baz', 'one'), ('baz', 'two')]
multi_index = pd.MultiIndex.from_tuples(index_tuples, names=['first', 'second'])

data = {'A': [1, 3, 5, 7],
        'B': [2, 4, 6, 8]}
df2 = pd.DataFrame(data, index=multi_index)

df_stacked = df2.stack()
df_stacked
```

3) Unstack

![](reshaping_unstack.png)
![](reshaping_unstack_0.png)
![](reshaping_unstack_1.png)

```{code-cell}
df_stacked.unstack()

# df_stacked.unstack(0)  or  df_stacked.unstack('first')
# df_stacked.unstack(1)  or  df_stacked.unstack('second')
```

4) Melt

![](reshaping_melt.png)

```{code-cell}
df3 = pd.DataFrame({'first': ['John', 'Mary'],
                    'last': ['Doe', 'Bo'],
                    'height': [5.5, 6.0],
                    'weight': [130, 150]})
                    
df3.melt(id_vars=['first', 'last'])
```

**Multiple Dataframes**

Concatenating two DataFrames in pandas is the process of combining them together to create a single DataFrame. This can be done either by concatenating along rows, which results in vertically stacking the DataFrames, or by concatenating along columns, which results in horizontally expanding the DataFrame. The distinction lies in whether the DataFrames are being extended vertically (rows) or horizontally (columns). The `concat` function in pandas is used for this operation, allowing for flexible combination of DataFrames based on the desired axis.

```{code-cell}
df1 = pd.DataFrame({'A': [1, 3, 5],
                    'B': [2, 4, 6]})
df2 = pd.DataFrame({'A': [7, 9, 11],
                    'B': [8, 10, 12]})
```

```{code-cell}
pd.concat((df1, df2), axis=0, ignore_index=True)  # concatenate by rows
```

```{code-cell}
pd.concat((df1, df2), axis=1, ignore_index=True)  # concatenate by columns
```

Merging two DataFrames in pandas is akin to performing SQL joins. It involves combining datasets based on common columns or indices, resulting in a unified DataFrame. The process, achieved using the `merge` function, is conceptually similar to SQL joins, where you define key columns for matching and specify the type of join (inner, outer, left, right) to determine how non-matching entries are handled. This enables you to consolidate data from distinct sources into a cohesive DataFrame, much like SQL joins bring together information from different database tables.

```{code-cell}
df1 = pd.DataFrame({"name": ['Magneto', 'Storm', 'Mystique', 'Batman', 'Joker', 'Catwoman', 'Hellboy'],
                    'alignment': ['bad', 'good', 'bad', 'good', 'bad', 'bad', 'good'],
                    'gender': ['male', 'female', 'female', 'male', 'male', 'female', 'male'],
                    'publisher': ['Marvel', 'Marvel', 'Marvel', 'DC', 'DC', 'DC', 'Dark Horse Comics']})
df2 = pd.DataFrame({'publisher': ['DC', 'Marvel', 'Image'],
                    'year_founded': [1934, 1939, 1992]})
                    
pd.merge(df1, df2, how='inner', on='publisher')
```

### Methods

| Method | Paramethers | Description |
| :----: | :---------: | :---------: |
| `apply`           | func, axis=0                                  | Applies a function along an axis of the dataframe |
| `drop_duplicates` | subset*=None, inplace=False                   | Returns dataFrame with duplicate rows removed |
| `dropna`          | axis=0, subset*=None, inplace=False           | Removes missing values |
| `duplicated`      | subset*=None                                  | Returns boolean series denoting duplicate rows |
| `fillna`          | value=None, method=None, inplace=False        | Fills na/nan values using the specified method |
| `groupby`         | by=None                                       | Groups dataframe using a mapper or by a series of columns |
| `map`             | func                                          | Apples a function to a dataframe elementwise |
| `sort_values`     | by, axis=0, ascending=True, inplace=False     | Sorts by the values along either axis |

**Examples**

```{code-cell}
import numpy as np

df = pd.DataFrame({
  'Name': ['Alice', 'Alice', 'Alice', 'Bob', 'Bob', 'Charlie', 'David'],
  'Age': [22, 22, 22, 23, 23, 20, 19],
  'Grade': [85, 85, np.nan, 78, 69, 85, 92]})
```

```{code-cell}
df['Grade_sqrt'] = df['Grade'].apply(np.sqrt)
df
```

```{code-cell}
age_mapping = {True: 'Young', False: 'Old'}
df['Age_category'] = df['Age'] <= 22
df['Age_category'] = df['Age_category'].map(age_mapping)
df
```

```{code-cell}
df.sort_values(by='Age')
```

```{code-cell}
df.groupby('Age')['Grade'].mean()
```

```{code-cell}
df['Duplicated'] = df.duplicated(subset='Name')
df
```

```{code-cell}
df.drop_duplicates(subset='Name', inplace=True)
```
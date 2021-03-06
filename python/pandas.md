The Pandas Python Library
=========================

[Pandas](https://pandas.pydata.org) is an open-source, high-performance library providing easy-to-use data structures and data analysis tools. Here are some useful commands and code snippets that I commonly use

# I/O

## Comma Separated Values (csv) files

A common format for data files is the [Comma Separated Values, or CSV, file](https://www.howtogeek.com/348960/what-is-a-csv-file-and-how-do-i-open-it/). Pandas has a dedicated I/O function to handle reading and writing these files

### Reading a .csv
The Pandas function [read_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html) is dedicated to, as you may have guessed, reading CSV files. It is the Pandas function that I use the most, as it's one of the best ways to read data into a DataFrame

#### Simple example
```
> import pandas as pd
> fname = 'CH4_global_emissions_by_fuel.csv'
> df = pd.read_csv(fname, sep=',', header=0)
> df.head()
         fuel   em units         X1750         X1751  ...         X2013         X2014
0     biomass  CH4    kt  4.962775e+03  4.975328e+03  ...  1.173315e+04  1.167107e+04
1  brown_coal  CH4    kt  0.000000e+00  0.000000e+00  ...  9.261101e+01  9.286888e+01
2   coal_coke  CH4    kt  1.821954e-11  1.821954e-11  ...  2.049853e-09  2.069470e-09
3  diesel_oil  CH4    kt  0.000000e+00  0.000000e+00  ...  2.690578e+02  2.708000e+02
4   hard_coal  CH4    kt  1.275129e+01  1.275129e+01  ...  1.050331e+03  1.052788e+03

[5 rows x 268 columns]
```

By default, `sep` (the delimiter to use, str) is `','` and `header` (row number(s) to use as the column names, int or list of int) is `'infer'`, meaning the function will try to infer the names of the columns. At a minimum, I like to define both of these arguments. 

Another helpful argument for `read_csv` is `dtype`, which defines the data type for the entire DataFrame or specific columns, e.g. `{‘a’: np.float64, ‘b’: np.int32, ‘c’: ‘Int64’}`. 

Sometimes files contain metadata before and/or after the actual data. Here, the functions `skiprows` and `skipfooter` are extremely helpful. 
* `skiprows` (list-like, int or callable) specifies the line numbers to skip (0-indexed) or number of lines to skip (int) at the start of the file. 
* `skipfooter` (int, default 0) specifies the number of lines at the bottom of the file to skip. However, it is only supported by the Python parser engine (see `engine`). 

### Writing a .csv
Similar to `write_csv`, Pandas has a dedicated CSV writing function, [to_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html). 

#### Examples
```
> df.head()
         fuel   em units         X1750         X1751  ...         X2013         X2014
0     biomass  CH4    kt  4.962775e+03  4.975328e+03  ...  1.173315e+04  1.167107e+04
1  brown_coal  CH4    kt  0.000000e+00  0.000000e+00  ...  9.261101e+01  9.286888e+01
2   coal_coke  CH4    kt  1.821954e-11  1.821954e-11  ...  2.049853e-09  2.069470e-09
3  diesel_oil  CH4    kt  0.000000e+00  0.000000e+00  ...  2.690578e+02  2.708000e+02
4   hard_coal  CH4    kt  1.275129e+01  1.275129e+01  ...  1.050331e+03  1.052788e+03

[5 rows x 268 columns]

> f_out = 'to_csv_example.csv'
> df.to_csv(f_out, sep=',', header=True, index_label=False)
```

Similar to `read_csv`, the argument `sep` defines the delimiter to use when writing the file. Since this function is designed to write csv files, the default value is a comma (','). The boolean argument `header` determines whether or not to write the column names, and is `True` by default. However, for clarity and to ensure I know what the outcome of the function call will be, I like to specify the values for these arguments. 

Pandas DataFrames contain an `index` column (the column containing `0, 1, 2, 3, 4` to the right of `fuel` in the above example DataFrame). By setting the value of `index_label` to `False` (its `True` by default), this index column will not be written to the csv file. More documentation can be found [here](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html).


# Indexing and Slicing DataFrames
The ability to slice, dice, and subset Pandas DataFrames is extremely useful, and there are a few different ways to go about these operations. See the [Pandas User Guide](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html) for further details.

## `loc`
`loc` is primarily label-based, meaning it operates best when given things like column names and/or row values. `loc` will raise a `KeyError` when items are not found in the given DataFrame.

### Basic Examples

We'll start off by creating a simple DataFrame:
```
> import pandas as pd
> df = pd.DataFrame([[1, 2], [4, 5], [7, 8]],
...    index=['cobra', 'viper', 'sidewinder'],
...    columns=['max_speed', 'shield'])
>>> df
            max_speed  shield
cobra               1       2
viper               4       5
sidewinder          7       8
```
  
#### Getting Values

* Given a single label, a row is returned as a [Series](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.html):
  ```
  > df.loc['viper']
  max_speed    4
  shield       5
  Name: viper, dtype: int64
  ```

* Given a list of labels using `[[]]` returns a DataFrame:
  ```
  > df.loc[['viper', 'cobra']]
         max_speed  shield
  viper          4       5
  cobra          1       2
  ```

* The value of a specific row and column can be retrieved as such:
  ```
  >  df.loc['cobra', 'shield']
  2
  ```

* Conditional that returns a boolean Series:
  ```
  > df.loc[df['shield'] > 6]
              max_speed  shield
  sidewinder          7       8
  ```

* Conditional that returns a boolean Series with column labels specified:
  ```
  > df.loc[df['shield'] > 6, ['max_speed']]
              max_speed
  sidewinder          7
  ```

* Callable that returns a boolean Series:
  ```
  > df.loc[lambda df: df['shield'] == 8]
              max_speed  shield
  sidewinder          7       8
  ```

#### Setting Values

In addition to retrieving values and objects from a DataFrame, `loc` can also be used to set values.

* Set value for all items matching the list of labels:
  ```
  > df.loc[['viper', 'sidewinder'], ['shield']] = 50
  > df
              max_speed  shield
  cobra               1       2
  viper               4      50
  sidewinder          7      50
  ```

* Set the value of an entire row:
  ```
  > df.loc['cobra'] = 10
  > df
              max_speed  shield
  cobra              10      10
  viper               4      50
  sidewinder          7      50
  ```

* Set the value of an entire column:
  ```
  > df.loc[:, 'max_speed'] = 30
  > df
              max_speed  shield
  cobra              30      10
  viper              30      50
  sidewinder         30      50
  ```

* Set value for rows matching callable condition:
  ```
  > df.loc[df['shield'] > 35] = 0
  > df
              max_speed  shield
  cobra              30      10
  viper               0       0
  sidewinder          0       0
  ```

More examples can be found in the [Pandas API reference](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.loc.html)

### Real-world Examples
Below are some real-world examples that implement concepts described in the examples above, but tend to be a bit more complex.

* CMIP6 Emissions Freeze
  When setting the emission factors for various emission species for years >= 1970 to their 1970 value, `loc` was used to ensure the correct values were being changed for a given [CEDS](https://github.com/JGCRI/CEDS) iso, sector, and fuel. 
  
  Here is an example of the emission factor csv files being used:
  
  ```
  > import pandas as pd
  > fname = 'H.CO2_total_EFs_extended.csv'
  > df = pd.read_csv(fname, sep=',', header=0)
  > df
         iso                         sector        fuel    units  X1750  ...  X2010  X2011  X2012  X2013  X2014
  0      abw                  11A_Volcanoes     process  kt/1000    0.0  ...    0.0    0.0    0.0    0.0    0.0
  1      abw               11B_Forest-fires     process  kt/1000    0.0  ...    0.0    0.0    0.0    0.0    0.0
  2      abw              11C_Other-natural     process  kt/1000    0.0  ...    0.0    0.0    0.0    0.0    0.0
  3      abw  1A1a_Electricity-autoproducer     biomass    kt/kt    0.0  ...    0.0    0.0    0.0    0.0    0.0
  4      abw  1A1a_Electricity-autoproducer  brown_coal    kt/kt    0.0  ...    0.0    0.0    0.0    0.0    0.0
  ...    ...                            ...         ...      ...    ...  ...    ...    ...    ...    ...    ...
  55207  zwe         5D_Wastewater-handling     process  kt/1000    0.0  ...    0.0    0.0    0.0    0.0    0.0
  55208  zwe        5E_Other-waste-handling     process  kt/1000    0.0  ...    0.0    0.0    0.0    0.0    0.0
  55209  zwe              6A_Other-in-total     process  kt/1000    0.0  ...    0.0    0.0    0.0    0.0    0.0
  55210  zwe          6B_Other-not-in-total     process  kt/1000    0.0  ...    0.0    0.0    0.0    0.0    0.0
  55211  zwe           7A_Fossil-fuel-fires     process  kt/1000    0.0  ...    0.0    0.0    0.0    0.0    0.0
  ```
  
  We only want to overwrite combustion-related sectors. In order to do this, DataFrame rows were selected with very strict criteria. For this example, we will select France as the country, or `iso`, `1A2g_Ind-Comb-Construction` as the `sector`, and `brown_coal` as the `fuel`:
  ```
  > iso = `fra`
  > sector = '1A2g_Ind-Comb-Construction'
  > fuel = 'brown_coal'
  ```
  
  Since `iso`, `sector`, and `fuel` are their own columns, the following snippet using `loc` finds the row we are interested in:
  ```
  > df.loc[(df['iso'] == iso) & (df['sector'] == sector) & (df['fuel'] == fuel)]
         iso                      sector        fuel  units  ...     X2011     X2012     X2013     X2014
  16263  fra  1A2g_Ind-Comb-Construction  brown_coal  kt/kt  ...  1.152316  1.152316  1.152316  1.152316

  [1 rows x 269 columns]
  ```

## `iloc`
Unlike `loc`, which is primarily label-based, `iloc` is integer position based (from `0` to `length-1` of the axis) and is used for selection by position. However, it may also be used with a boolean array. `iloc` will raise an `IndexError` if a requested indexer is out-of-bounds, except in the case of slice indexers, which allow out-of-bounds indexing. 

### Basic Examples

We'll start off by creating a simple DataFrame from a dictionary:
```
> import pandas as pd
> mydict = [{'a': 1, 'b': 2, 'c': 3, 'd': 4},
...         {'a': 100, 'b': 200, 'c': 300, 'd': 400},
...         {'a': 1000, 'b': 2000, 'c': 3000, 'd': 4000 }]
> df = pd.DataFrame(mydict)
> df
      a     b     c     d
0     1     2     3     4
1   100   200   300   400
2  1000  2000  3000  4000
```

#### Indexing just the rows

* With a scalar integer:
  ```
  > type(df.iloc[0])
  <class 'pandas.core.series.Series'>
  > df.iloc[0]
  a    1
  b    2
  c    3
  d    4
  Name: 0, dtype: int64
  ```

* With a list of integers:
  ```
  > df.iloc[[0]]
     a  b  c  d
  0  1  2  3  4
  > type(df.iloc[[0]])
  <class 'pandas.core.frame.DataFrame'>
  ```

  ```
  > df.iloc[[0, 1]]
       a    b    c    d
  0    1    2    3    4
  1  100  200  300  400
  ```

* With a *slice* object:
  ```
  > df.iloc[:3]
        a     b     c     d
  0     1     2     3     4
  1   100   200   300   400
  2  1000  2000  3000  4000
  ```

* With a boolean mask the same length as the index:
  ```
  > df.iloc[[True, False, True]]
        a     b     c     d
  0     1     2     3     4
  2  1000  2000  3000  4000
  ```

* With a callable, useful in method chains. The x passed to the `lambda` is the DataFrame being sliced. This selects the rows whose index label even:
  ```
  > df.iloc[lambda x: x.index % 2 == 0]
        a     b     c     d
  0     1     2     3     4
  2  1000  2000  3000  4000
  ```

#### Indexing both axes

You can mix the indexer types for the index and columns. Use `:` to select the entire axis.

* With scalar integers:
  ```
  > df
        a     b     c     d
  0     1     2     3     4
  1   100   200   300   400
  2  1000  2000  3000  4000
  > df.iloc[0, 1]
  2
  ```

* With lists of integers:
  ```
  > df.iloc[[0, 2], [1, 3]]
        b     d
  0     2     4
  2  2000  4000
  ```

* With *slice* objects:
  ```
  > df.iloc[1:3, 0:3]
        a     b     c
  1   100   200   300
  2  1000  2000  3000
  ```

* With a boolean array whose length matches the columns:
  ```
  > df.iloc[:, [True, False, True, False]]
        a     c
  0     1     3
  1   100   300
  2  1000  3000
  ```

* With a callable function that expects the Series or DataFrame:
  ```
  > df.iloc[:, lambda df: [0, 2]]
        a     c
  0     1     3
  1   100   300
  2  1000  3000
  ```

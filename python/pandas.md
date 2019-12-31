# The Pandas Python Library

[Pandas](https://pandas.pydata.org) is an open-source, high-performance library providing easy-to-use data structures and data analysis tools. Here are some useful commands and code snippets that I commonly use

## I/O

### Comma Separated Values (csv) files

A common format for data files is the [Comma Separated Values, or CSV, file](https://www.howtogeek.com/348960/what-is-a-csv-file-and-how-do-i-open-it/). Pandas has a dedicated I/O function to handle reading and writing these files

#### Reading a .csv
The Pandas function [read_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html) is dedicated to, as you may have guessed, reading CSV files. It is the Pandas function that I use the most, as it's one of the best ways to read data into a DataFrame

##### Simple example
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

#### Writing a .csv
Similar to `write_csv`, Pandas has a dedicated CSV writing function, [to_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html). 

##### Simple example
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

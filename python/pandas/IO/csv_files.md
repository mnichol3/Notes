# Pandas and .csv file operations

Comma Separated Values (csv) files are an extremely common data file format. Pandas has dedicated csv I/O functions that make reading & writing data a breeze

## Reading a CSV

The [`read_csv`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html) function reads a csv file into a DataFrame:

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
Helpful keyword args:
  * `sep`: Delimiter that separates data values in the file (*str, optional*; default is `','`)
  * `header`: Rrow to use as column names (*int, list of int; optional*, default is `0`)
  * `names`: List of column names to use (*array-like, optional*)
  * `usecols`: Read only a subset of column (*list-like or callable, optional*)
  * `dtype`: Data type for data or columns (*Type name or dict of column -> type, optional*)
  

## Writing a CSV

The [`to_csv`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html) function writes a DataFrame to a .csv file:

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
> df.to_csv(f_out, sep=',', header=True, index=False)
```
Helpful keyword args:
  * `sep`: Delimiter that separates data values in the file (*str, optional*; default is `','`)
  * `header`: Write out the column names (*bool or list of str*, default `True`)
  * `index`: Write the index column (*bool*, default `True`)
  * `na_rep`: Missing data representation (*str*, default `‘’`)
  
  
### Reference
* [`read_csv`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)
* [`to_csv`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html)
  
  

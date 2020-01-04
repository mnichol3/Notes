# The `ls` Command

The `ls` command lists directory contents

## Synopsis
`ls [OPTION] ... [FILE]`

## Arguments 
 * **`-a, --all`**
   * Do not ignore entries starting with `.`
  * **`-A, --almost-all`**
   * Do not list implied `.` and `..`
 * **`-C`**
   * List entries by columns
 * **`-d, --directory`**
   * List directory entries instead of contents
 * **`-l`**
   * Use long listing format
 * **`-o`**
   * Like **`l`**, but do not list group information
 * **`-R`**
   * List subdirectories recursively
 * **`-x`**
   * List entries by lines instread of columns
 * **`-1`**
   * List one file per line

## Examples

* **List files in current directory**:
  ```
  > ls 
  2014-01.csv  2014-08.csv  2015-03.csv  2015-10.csv 2016-05.csv  2016-12.csv  2017-07.csv
  2014-02.csv  2014-09.csv  2015-04.csv  2015-11.csv 2016-06.csv  2017-01.csv  2017-08.csv
  2014-03.csv  2014-10.csv  2015-05.csv  2015-12.csv 2016-07.csv  2017-02.csv  2017-09.csv
  ```
  
  ```
  > ls -l
  -rwxr-xr-x 1 mnichol3 mnichol3 123198269 Jan  3 22:14 2014-01.csv
  -rwxr-xr-x 1 mnichol3 mnichol3 112404190 Jan  3 22:14 2014-02.csv
  -rwxr-xr-x 1 mnichol3 mnichol3 131980733 Jan  3 22:14 2014-03.csv
  -rwxr-xr-x 1 mnichol3 mnichol3 126720333 Jan  3 22:14 2014-04.csv
  -rwxr-xr-x 1 mnichol3 mnichol3 130833607 Jan  3 22:14 2014-05.csv
  -rwxr-xr-x 1 mnichol3 mnichol3 132228424 Jan  3 22:14 2014-06.csv
  -rwxr-xr-x 1 mnichol3 mnichol3 136778208 Jan  3 22:14 2014-07.csv
  -rwxr-xr-x 1 mnichol3 mnichol3 133176537 Jan  3 22:14 2014-08.csv
  -rwxr-xr-x 1 mnichol3 mnichol3 122791378 Jan  3 22:14 2014-09.csv

  ```
  
* **List files in different directory**
  ```
  ls /path/to/dir
  ls -l /path/to/dir
  ```
  
* **List sudbirectories in current directory**
  ```
  ls -d */
  ```
  
* **List 20 newest files in current directory**
  ```
  ls -ltr|tail -20
  ```
  
* **List files with extentsion** (`.dat` in this example)
  ```
  ls -l | grep '\.dat$'
  ```
  
* **Count files in current directory**
  ```
  ls -l | wc -l
  ```
  
* **Count files in current directory with extension** (`.dat` in this example)
  ```
  ls -l | grep '\.dat$' | wc -l
  ```

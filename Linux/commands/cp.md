# The `cp` Command

The `cp` command copies files and directories

## Synopsis
`cp [OPTION] ... source dest`

## Arguments 
 * **`-b`**
   * Make a backup of each existing file destination
 * **`-f, --force`**
   * If an existing destination file cannot be opened, remove it and try again (redundant if the **`-n`** option is used)
 * **`-i, --interactive`**
   * Prompt before overwriting (overrides a previous **`-n`** option)
 * **`-n, --no-clobber`**
   * Do not overwrite an existing file
   
 **Note:** If you specify more than one of **`-i`**, **`-f`**, **`-n`**, on the the final one takes effect.
 
 * **`-r`**
   * Recursive move; move the current directory and its contents, including any subdirectories
 * **`--strip-trailing-slashes`**
   * Remove any trailing slashes from each *SOURCE* argument
 * **`-S, --suffix`**
   * Override the usual backup siffux
 * **`-t, --target-directory`**
   * Move all *SOURCE* arguments into *DIRECTORY*
 * **`-T, --no-target-directory`**
   * Treat *DEST* as a normal file
 * **`-u, --update`**
   * Copy only when the *SOURCE* file is newer than the destination file or when the destination file is missing
 * **`-v, --verbose`**
   * Verbose output; explain the operations being executed
 * **`--help`**
   * Desplay help

## Examples
* **Copy a single file** from `/path/to/current_dir/` to `/path/to/new_dir/`:
  ```
  cp /path/to/current_dir/target_file.txt /path/to/new_dir/
  ```
  
* **Copy multiple files** from `/path/to/current_dir/` to `/path/to/new_dir/`:
  ```
  cp /path/to/current_dir/*.txt /path/to/new_dir/
  cp /path/to/current_dir/* /path/to/new_dir/
  ```
  
* **Copy directory & subdirectories** from `/path/to/current_dir/` to `/path/to/new_dir/`:
  ```
  cp -r /path/to/current_dir/target_dir /path/to/new_dir/
  cp -r /path/to/current_dir/* /path/to/new_dir/
  ```
  
  
## References
* https://linux.die.net/man/1/cp

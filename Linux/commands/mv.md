# The `mv` Command

The `mv` command is extremely useful, as it not only allows you to move files between directories, but also allows you to rename files. 

## Synopsis
`mv [OPTION] ... source dest`

## Arguments 
 * **`-b`**
   * Make a backup of each existing file destination
 * **`-f, --force`**
   * Do not prompt before overwriting
 * **`-i, --interactive`**
   * Prompt before overwriting
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
   * Move only when the *SOURCE* file is newer than the destination file or when the destination file is missing
 * **`-v, --verbose`**
   * Verbose output; explain the operations being executed
 * **`--help`**
   * Desplay help

## Examples

### Moving Files
* **Moving a single file from one directory to another**
  
  Let's start with a simple example by moving `target_file.txt` from `/path/to/current_dir/` to `/path/to/new_dir/`:
  ```
  mv /path/to/current_dir/target_file.txt /path/to/new_dir/
  ```
  
* **Moving multiple files from one directory to another**
  
  Say we want to move every `.txt` file from `/path/to/current_dir/` to `/path/to/new_dir/`. We can accomplish this with the following command:
  ```
  mv /path/to/current_dir/*.txt /path/to/new_dir/
  ```
  
* **Moving a directory and its subdirectories**

  In order to move a directory and its subdirectories, we need to pass the `-r` argument:
  ```
  mv -r /path/to/current_dir/* /path/to/new_dir/
  ```
  This command moves *everything* in `current_dir` to `new_dir`. 
  

### Renaming Files

* **Renaming a single file**
  ```
  mv oldfile.txt newfile.txt
  ```

* **Renaming multiple files**
  
  Although `mv` is not a dedicated file renaming command, it is still able to rename files through its functionality. Essentially, the contents of `oldfile.txt` are moved into a *new* file, and that new file is then named `newfile.txt`. However, things become much more complicated when it comes to renaming multiple files with `mv`. I recommend a script or the `rename` command to handle renaming multiple files.
  

## References
* https://linux.die.net/man/1/mv

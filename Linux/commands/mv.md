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

Notes and examples of various loops from [tldp](https://tldp.org/LDP/abs/html/loops1.html)

# Loops - *For* loop
## Basic structure
```bash
for arg in list
do
  command(s)
done
```


## Example 1 - Basic *for* loops
```bash
#!/bin/bash
# List the planets.

for planet in Mercury Venus Earth Mars Jupiter Saturn Uranus Neptune Pluto
do
  echo $planet
done

exit 0
```


## Example 2 - *for* loop with two parameters in each [list] element
```bash
#!/bin/bash
# Planets revisited.

# Associate the name of each planet with its distance from the sun.

for planet in "Mercury 36" "Venus 67" "Earth 93" "Mars 142" "Jupiter 483"
do
  set -- $planet  #  Parses variable "planet" and sets positional params.
  
  #  The "--" prevents nasty surprises if $planet is null or begins with a dash.
  
  #  May need to save original positional parameters since they may have gotten overwritten.
  #  One way of doing this is to use an array:
  #      original_params=("$@")
  
  echo "$1    $2,000,000 miles from the sun"
  # -------- two  tabs -------- concatenate zeroes onto parameter $2
  done 
  
  exit 0
```


## Example 3 - Operating on a file list contained in a variable
```bash
#!/bin/bash
# fileinfo.sh

FILES="/usr/sbin/accept
/usr/sbin/pwck
/usr/sbin/chroot
/usr/bin/fakefile
/sbin/badblocks
/sbin/ypbind"       # List of files you are curious about.
                    # Threw in a dummy file, /usr/bin/fakefile
                    
echo

for file in $FILES
do
  if [ ! -e "$file" ]         #  Check if file exists
  then
    echo "$file does not exist."; echo
    continue
  fi                          # On to the next file.
  
  ls -l $file | awk '{ print $8 "     file size: " $5 }'  # Print 2 fields.
  whatis `basename $file`     # File info.
  #  Note that the whatis database needs to have been set up for this to work.
  #  To do this, run /usr/bin/makewhatis as root.
  echo
done

exit 0
```


## Example 4 - Multiple ways to count to 10
```bash
#!/bin/bash
# Lets count to 10

echo 

# Standatd syntax ...
for a in 1 2 3 4 5 6 7 8 9 10
do
  echo -n "$a "
done

echo; echo

# +=========================================+

# Using "seq" ...
for a in `seq 10`
do
  echo -n "$a "
done

echo; echo

# +=========================================+

# Using brace expansion ...
# Bash version 3+.
for a in {1..10}
do
  echo -n "$a "
done

echo; echo

# +=========================================+

# Using C-like syntax ...
LIMIT=10

for ((a=1; a <= LIMIT ; a++))        # Double parenthesis, and naked "LIMIT"
do
  echo -n "$a "
done

echo; echo

# +=========================================+

# Using C "comma operator" to increment two variables simultaneously ...
for ((a=1, b=1; a <= LIMIT ; a++, b++))
do   # The comma concatenates operations.
  echo -n "$a-$b "
done

echo; echo

exit 0
```

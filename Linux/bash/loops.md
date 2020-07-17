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

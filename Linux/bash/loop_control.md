Notes and examples of various loop control from [tldp](https://tldp.org/LDP/abs/html/loopscontrol.html)

# Effects of *break* and *continue* in a loop

## Example 1 - *break*
```bash
#!/bin/bash

LIMIT=19

echo
echo "Printing Numbers 1 through 20 (but not 3 and 11)."

i=0

while [ $i -le "$LIMIT" ]
do
  i=$(($i+1))
  
  if [ "$i" -eq 3 ] || [ "$i" -eq 11 ]   # Excludes 3 and 11.
  then
    continue    # Skip the rest of this perticular iteration.
  fi
  
  echo -n "$i"  # This will not execute for 3 and 11.
done
  
echo; echo
  
exit 0
```


## Example 2 - *continue*
```bash
#!/bin/bash

LIMIT=19

echo
echo "Printing Numbers 1 through 20, but something happens after 2."

i=0

while [ $i -le "$LIMIT" ]
do
  i=$(($i+1))
  
  if [ "$i" -le "$LIMIT" ]
  then
    break    # Skip the rest of loop.
  fi
  
  echo -n "$i"
done
  
echo; echo
  
exit 0
```


## Example 3 - Breaking out of multiple loop levels
```bash
#!/bin/bash
# break-levels.sh: Breaking out of loops.

# "break N" breaks out of N level loops.

for outerloop in 1 2 3 4 5
do
  echo -n "Group $outerloop:   "

  # --------------------------------------------------------
  for innerloop in 1 2 3 4 5
  do
    echo -n "$innerloop "

    if [ "$innerloop" -eq 3 ]
    then
      break  # Try   break 2   to see what happens.
             # ("Breaks" out of both inner and outer loops.)
    fi
  done
  # --------------------------------------------------------

  echo
done  

echo

exit 0
```


## Example 4 - Continuing at a higher loop level
```bash
#!/bin/bash
# The "continue N" command, continuing at the Nth level loop.

for outer in I II III IV V           # outer loop
do
  echo; echo -n "Group $outer: "

  # --------------------------------------------------------------------
  for inner in 1 2 3 4 5 6 7 8 9 10  # inner loop
  do

    if [[ "$inner" -eq 7 && "$outer" = "III" ]]
    then
      continue 2  # Continue at loop on 2nd level, that is "outer loop".
                  # Replace above line with a simple "continue"
                  # to see normal loop behavior.
    fi  

    echo -n "$inner "  # 7 8 9 10 will not echo on "Group III."
  done  
  # --------------------------------------------------------------------

done

echo; echo

exit 0
```

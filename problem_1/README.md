# Problem 1

> See the problem_1 subdirectory.

A researcher has inadvertently renamed all their 100 data files with the wrong file extension and doesn’t know how to change them back. Show you can rename the files to have a `.dat` file extension and explain to the researcher how they can do this themselves if they make this mistake again.
## Solution

The `mv` command line is is ideal for this problem. To execute this task, at the command prompt, enter:

``` bash
for f in *.csv; do     mv -- "$f" "${f%.csv}.dat"; done
```

# Problem 2

> See the problem_2 subdirectory.

A researcher you have met regularly runs several hundred samples through an analysis machine over the weekend. Most of the time each sample run completes fully, writing 100 values into a numbered file for that sample. Occasionally, a sample run fails and fewer than 100 values are written to a file.

Can you show this researcher how to quickly identify the sample files that have fewer than 100 values?

## Solutions

> Command prompt based solutions!

Using `wc` command:

``` bash
wc -w values*
```

or using the `awk` command:

``` bash
for f in values*; do    awk '{ if (NF < 100) print NF, FILENAME}' $f; done
```
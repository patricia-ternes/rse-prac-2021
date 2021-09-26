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

### Using the `wc` command

`wc` (abbreviation for word count) is a Linux command that displays some useful information for a file. The syntax is:

```bash
wc OPTION FILE
```

The `OPTION` select what information will be printed. The following options are available:

* `-l` number of lines
* `-w` number of words
* `-m` number of characters
* `-c` number of bytes
* `-L` length of the longest line

In this Problem, the values were written in columns and organised in files with names `valuesX`, where X=[1, 300]. So, the following command will return a long list with the number of words (in this case is equal to columns) and the correspondent name file.

``` bash
wc -w values*
```

The output:

```bash
   100 values1
   100 values10
   100 values100
   100 values101
   100 values102
   ... ...
   100 values95
   100 values96
   100 values97
   100 values98
   100 values99

```

The researcher must manually go through the list and check which file does not have 100 words. This solution is simple to apply, but it requires a manual analysis that, depending on the number of files, can become an impractical task.

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

### Using the `awk` command

The `awk` command (abbreviation for Aho, Weinberger and Kernighan - original authors' names) is a complete text manipulation toolkit. You can find [here](https://www.gnu.org/software/gawk/manual/gawk.html) a complete guide for the `awk` command.

For instance, we are interested in obtaining the name of files that have less than 100 columns. So, lets start with a command that will return the number of columns for the file `value1`:

```bash
awk '{print NF, FILENAME}' values1
```

where:

* `NF`: [Built-In variable] count of the number of fields (columns)
* `FILENAME`: [Built-In variable] name of the file

The output will be:

```bash
100 values1
```

We can add an `if statement` to print the output only in cases where the file has less than 100 columns. The following command would not return any value, since as seen above, the values1 file has 100 columns.

``` bash
awk '{ if (NF < 100) print NF, FILENAME}' values1
```

Finally, we can use a loop to go through all the desired files. The final command is:

``` bash
for f in values*; do    awk '{ if (NF < 100) print NF, FILENAME}' $f; done
```

For this problem, the output is:

```bash
99 values44
```

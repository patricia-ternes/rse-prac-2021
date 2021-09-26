# Problem 1

> See the problem_1 subdirectory.

A researcher has inadvertently renamed all their 100 data files with the wrong file extension and doesn’t know how to change them back. Show you can rename the files to have a `.dat` file extension and explain to the researcher how they can do this themselves if they make this mistake again.
## Solution

The `mv` command line is is ideal for this problem. To execute this task, at the command prompt, enter:

``` bash
for f in *.csv; do     mv -- "$f" "${f%.csv}.dat"; done
```

## Explanation

To rename one file the mv command is used in the form:

``` bash
mv [option] [filename] [new-filename]
```

Some common options are `-i` (prompt before overwrite) and `-n` (do not overwrite an existing file). You can enter `mv --help` at the command prompt to see more available options.

For example, to update the `datafile1.csv` name to `datafile1.dat` at the command prompt, enter:

``` bash
mv datafile1.csv datafile1.dat
```

But if you want to keep the original file, you can use the `-n` option, so after enter

``` bash
mv -n datafile1.csv datafile1.dat
```

in this case, both files `datafile1.csv` and `datafile1.dat` will be available after last operation.

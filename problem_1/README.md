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
To rename multiple files with the `mv` command line is necessary to use a Bash loop. The basic loop syntax is:

```bash
for item in list; do
    [operation];
done
```

* line 1: creates a `for` loop that iterates over every `item` existent in the `list`
* line 2: apply some operation in every `item` variable
* line 3: indicates the end of the loop-statement

For instance, the `list` should have the name of all files that have a `csv` file extension, this can be obtained using the `*` (*wildcard* that represents any sequence of characters), i.e.,

```bash
for f in *.csv
```

Here the `item` was renamed `f` short for (file). The desired operation is to apply `mv` command for every item (here `f`), so the operation should be something like

```bash
mv "$f" "${f%.csv}.dat"
```

- `mv`: is the basic operation
- `"$f"`: represent a different filename in every iteration. The `"$ "` is used to reference a bash variable.
- `"${f%.csv}.dat"`: represent a different new-filename in every iteration. The new-filename is composed by the original filename stored in the `f` variable, but without the `.csv` part. Finally a `.dat` is add at the end.

The above operation work specially in cases where the filenames do not have spaces or *strange* characters, and neither start with the character `-`. I recommend adding the `--` option to make the `mv` operation more robust. This will help to change filenames that start with the `-` character. Therefore the complete code is:

``` bash
for f in *.csv; do
     mv -- "$f" "${f%.csv}.dat"; 
done
```

or in one line

``` bash
for f in *.csv; do     mv -- "$f" "${f%.csv}.dat"; done
```

## Additional solutions

If the problem involves more *complex* filenames, then a different solution may be necessary. I cite here two options:

1. Using the `sed` (see more about [here](https://www.gnu.org/software/sed/manual/sed.html))
2. Using  Perl `rename` (see more about [here](https://perldoc.perl.org/functions/rename))

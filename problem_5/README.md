# Problem 5

A client wishes to put information on our Omniglobe (https://arcscience.com/omniglobe-technology/). 

They provided a series of NetCDF files with names like: ozone_8dec2009.nc, ozone_7dec2009.nc, ozone_9dec2009.nc, ... etc.

A python script is used to access the files, extract some data and produce 2D images in PNG format.
The software for the Omniglobe:

- scans the contents of a folder
- generates an animated sequence from the PNG files contained in the directory.

This fragment of the Python script sets up the filenames to be written.

```python
# Build up filename
VarName= "Ozone_"
TimeStamp = "2001-01-01" # this could be in the nc file
Frame = str("%04d"%simhour)
MetaData = VarName+TimeStamp+"_"+Frame
fname_out = Home+MetaData+".png"

# create the file
savefig(fname_out,bbox_inches="tight",pad_inches=0.0)
```

In the script fragment above:

1. Can you determine the content of the `fname_out` variable?
2. What information is missing?

## Solution

The `fname_out` is a string `variable`. This variable is used to set a name for the figure created in the last code line. It is not possible to completely define the string that this variable returns, since two variables have not been defined:

- `simhour`
- `Home`

We can however estimate a generic format taking into account some parts of the code.

### `simhour` generic estimation

The `simhour` appears the first time in following piece of the code:

```python
Frame = str("%04d"%simhour)
```

The `str("%04d"%)` convert the `simhour` variable in a string with at least four integer number. Therefore, the `simhour` should be assigned as a number (real or integer). Some examples for the `simhour` and `Frame` variables:

|`simhour` value |`simhour` type |`Frame` value | `Frame` type |
| :--: | :--:    | :--: | :--:   |
| 1    | integer | 0001 | string |
| 1.9  | real    | 0001 | string |
| 123  | integer | 0123 | string |
| 1234 | integer | 1234 | string |

### `Home` generic estimation

The `Home` appears the first time in following piece of the code:

```python
fname_out = Home+MetaData+".png"
```

The `Home` is being directly concatenated with two other string variables, therefore the `Home` should be assigned as a string variable. Assuming the variable stores the location where the figure will be saved, a possible example for the `Home` variable is: `'/home/User/Documents/Figures/'`.

### `fname_out` generic estimation

Giving arbitrary values for the two missing variables, we can see the final format of the content stored in the variable. Considering:

- `simhour` = 1
- `Home` = `'/home/User/Documents/Figures/'`

the content of the `fname_out` variable will be:
```bash
/home/User/Documents/Figures/Ozone_2001-01-01_0001.png
```

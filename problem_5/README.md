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

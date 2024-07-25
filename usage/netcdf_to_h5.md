# netcdf_to_cvm

## Overview

The `netcdf_to_h5` tool is a utility tool for converting an existing CVM-compliant netCDF file to HDF5 format.

In this tutorial, we will demonstrate how to run `netcdf_to_h5` on a CVM netCDF file `Cascadia-ANT+RF-Delph2018.r0.1.nc` to convert it to HDF5 format.

## Steps

1. **Navigate to the model directory**

   Change your directory to the location of the model file:

   ```
   cd sample-files/Cascadia-ANT+RF-Delph2018
   ```

   and make sure the input netCDF file, **Cascadia-ANT+RF-Delph2018.r0.1.nc**, exists.

2. **Run the netcdf_to_h5 tool**

   Use the **netcdf_to_h5** tool to convert the `CCascadia-ANT+RF-Delph2018.r0.1.nc` file HDF5 format and save it as `Cascadia-ANT+RF-test.h5`:

   ```

   ../../src/netcdf_to_h5.py -d Cascadia-ANT+RF-Delph2018.r0.1.nc -o Cascadia-ANT+RF-test

   ```

   **Note**: The HDF5 files have **".h5"** extension. The converter script will add it if it is missing from your **-o** file name.

   **Command breakdown**

   - `-d Cascadia-ANT+RF-Delph2018.r0.1.nc`: Specifies the name of the netcdf input file.
   - `-o Cascadia-ANT+RF-test`: Specifies the name of the output file (**the file extension of .h5 is optional**).

   The `netcdf_to_h5` output, as shown below, informs us of how the conversion is going and it compares the input/output datasets:
   We can ignore the **Data mismatch for variable** warning since the resulting **Max difference** is zero and is an indicative of comparing float values.

   ```
   [INFO] Cascadia-ANT+RF-Delph2018.r0.1.nc is a netCDF file
   [INFO] Data for variable 'easting' matches between netCDF and HDF5.
   [INFO] Data for variable 'northing' matches between netCDF and HDF5.
   [WARN] Data mismatch for variable 'vs' between netCDF and HDF5.
   [WARN] Max difference: 0.0
   [INFO] Converted Cascadia-ANT+RF-Delph2018.r0.1.nc to Cascadia-ANT+RF-test.h5
   ```

```

```

# netcdf_to_h5

## Overview

The `netcdf_to_h5` tool is a utility tool for converting an existing CVM-compliant netCDF file to CVM-compliant HDF5 format.

In this tutorial, we will demonstrate how to run `netcdf_to_h5` on the CVM netCDF file `Cascadia-ANT+RF-Delph2018.r0.1.nc` to convert it to HDF5 format.

## Steps

1. **Navigate to the model directory**

   Change your directory to the location of the model file:

   ```sh
   cd sample-files/Cascadia-ANT+RF-Delph2018
   ```

   and make sure the input netCDF file, **Cascadia-ANT+RF-Delph2018.r0.1.nc**, exists.

2. **Run the netcdf_to_h5 tool**

   Use the **netcdf_to_h5** tool to convert the `Cascadia-ANT+RF-Delph2018.r0.1.nc` file HDF5 format and save it as `Cascadia-ANT+RF-test.h5`:

   ```sh

   ../../src/netcdf_to_h5.py -i Cascadia-ANT+RF-Delph2018.r0.1.nc -g MODEL -s VELOCITY -o Cascadia-ANT+RF-test

   ```

   **Note**: The HDF5 files have **".h5"** extension. The converter script will add it if it is missing from your **-o** file name.

   **Command breakdown**

   - `-i Cascadia-ANT+RF-Delph2018.r0.1.nc`: Specifies the name of the netcdf input file.
   - `-g MODEL`: informs the tool that the name of the main HDF5 group for this data is `MODEL`.
   - `-s VELOCITY`: is an optional argument and informs the tool that the name of the subgroup under the main group is `MODEL`. As a result, the netCDF dataset in the HDF5 will be stored under /MODEL/VELOCITY.
   - `-o Cascadia-ANT+RF-test`: Specifies the name of the output file (**the file extension of .h5 is optional**).

   The `netcdf_to_h5` output, as shown below, informs us of how the conversion is going.

   ```sh
   [INFO] Cascadia-ANT+RF-Delph2018.r0.1.nc is a netCDF file
   [WARN] Variable 'depth' already exists in the subgroup 'VELOCITY'. Skipping.
   [WARN] Variable 'latitude' already exists in the subgroup 'VELOCITY'. Skipping.
   [WARN] Variable 'longitude' already exists in the subgroup 'VELOCITY'. Skipping.
   [INFO] Conversion from Cascadia-ANT+RF-Delph2018.r0.1.nc to Cascadia-ANT+RF-test.h5 under '/MODEL/VELOCITY' completed successfully.

   ```

   We can run the `show_file_structure` toll and the the data structure of the output file:

`../../src/show_file_structure.py`
`Enter the path to the input file (HDF5 or netCDF):` Cascadia-ANT+RF-test.h5

```sh
File Name: Cascadia-ANT+RF-test.h5
File Size: 421678 bytes
File Type: HDF5

HDF5 File Structure:
├── MODEL
│ ├── VELOCITY
│ │ ├── depth
│ │ ├── easting
│ │ ├── latitude
│ │ ├── longitude
│ │ ├── northing
│ │ ├── vs

```

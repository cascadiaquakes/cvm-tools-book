# netcdf_to_cvm

## Overview

The `netcdf_to_cvm` tool is a utility tool for converting an existing netCDF CVM file to the corresponding CVM-compliant netCDF file. This tool will add any missing CVM attributes based on the provided metadata files.

In this tutorial, we will demonstrate how to run `netcdf_to_cvm` on a CVM netCDF file `Cascadia-ANT+RF-test-missing.nc` that is missing some CVM metadata attributes.

## Steps

1. **Navigate to the Model Directory**

   Change your directory to the location of the model file:

   ```bash
   cd sample-files/Cascadia-ANT+RF-Delph2018
   ```

2. **Run the netcdf_to_cvm Script**

   Use the **netcdf_to_cvm** tool to update the `Cascadia-ANT+RF-test-missing.nc` file and add the missing parameters to it:

   ```bash
   ../../src/netcdf_to_cvm.py -d Cascadia-ANT+RF-Delph2018.r0.1.nc -g Cascadia-ANT+RF_global_meta.txt -m Cascadia-ANT+RF_meta.txt -o Cascadia-ANT+RF-test-updated
   ```

**Command Breakdown**

- `-d Cascadia-ANT+RF-Delph2018.r0.1.nc`: Specifies the name of the input file to check.
- `-g Cascadia-ANT+RF_global_meta.txt`: Specifies the global metadata file.
- `-m Cascadia-ANT+RF_meta.txt`: Specifies the variables metadata file.
- `-o Cascadia-ANT+RF-test-updated.nc`: Specifies the name of the output file (**do not include a file extension**).

The `netcdf_to_cvm` output, as shown below, informs us of what it needed to update/add in the file:

```bash
[INFO] Added the missing global attribute data_layout: 'vertex'
[INFO] Added the missing vs attribute data_source: 'data-derived'
[INFO] Added the missing easting attribute standard_name: 'easting'
[INFO] Added the missing easting attribute long_name: 'easting; UTM'
[INFO] Added the missing easting attribute units: 'm'
[INFO] Added the missing northing attribute long_name: 'northing; UTM'
[INFO] Added the missing northing attribute units: 'm'
[INFO] Added the missing northing attribute standard_name: 'northing'
```

## Verification

Use the **netCDF_summary_info** utility tool to verify that the listed updates have taken place.

```bash
../../src/netCDF_summary_info.py
Enter the path to the NntCDF file:
```

For example:

**From `Cascadia-ANT+RF-test-missing.nc` summary output**:

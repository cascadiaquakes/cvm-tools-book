
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

   Use the following command to update the `Cascadia-ANT+RF-test-missing.nc` file and add the missing parameters to it:

   ```bash
   ../../src/netcdf_to_cvm.py -i Cascadia-ANT+RF-test-missing.nc -g Cascadia-ANT+RF_global_meta.txt -m Cascadia-ANT+RF_meta.txt -o Cascadia-ANT+RF-test-updated.nc
   ```

**Command Breakdown**

- `-i Cascadia-ANT+RF-test-missing.nc`: Specifies the name of the input file to convert.
- `-g Cascadia-ANT+RF_global_meta.txt`: Specifies the global metadata file.
- `-m Cascadia-ANT+RF_meta.txt`: Specifies the variables metadata file.
- `-o Cascadia-ANT+RF-test-updated.nc`: Specifies the name of the output file.

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

Now, by running the `netCDF_summary_info` utility tool twice, once for the input file, `Cascadia-ANT+RF-test-missing.nc`, and once for the output file, `Cascadia-ANT+RF-test-updated.nc`, and comparing the summary outputs, we can confirm that the listed updates have taken place.

```bash
../../src/netCDF_summary_info.py
Enter the path to the NetCDF file:
```

For example:

**From `Cascadia-ANT+RF-test-missing.nc` summary output**:

```bash
  - vs (dimensions: ('depth', 'latitude', 'longitude'), shape: (84, 46, 25))
    - _FillValue: nan
    - variable: vs
    - long_name: Shear-wave velocity
    - display_name: S Velocity (km/s)
    - units: km.s-1
    - coordinates: easting northing
    - grid_mapping: latitude_longitude
```

**From `Cascadia-ANT+RF-test-updated.nc` summary output**:

```bash
  - vs (dimensions: ('depth', 'latitude', 'longitude'), shape: (84, 46, 25))
    - _FillValue: nan
    - variable: vs
    - long_name: Shear-wave velocity
    - display_name: S Velocity (km/s)
    - units: km.s-1
    - grid_mapping: latitude_longitude
    - data_source: data-derived <-----< added attribute
    - coordinates: easting northing
```

We see that `data_source: data-derived` is added to the output netCDF file.

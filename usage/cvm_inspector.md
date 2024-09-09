# cvm_inspector

The `cvm_inspector` tool is a utility tool for checking the metadata, dimensions, coordinates, and variables of a netCDF file. The tool provides a comprehensive inspection of the file and ensures compliance with the CF convention.

In this tutorial, we will demonstrate how to run `netcdf_to_cvm` on the CVM netCDF file we created with the <a href="cvm_writer.html">cvm_writer tool</a> tool (`Cascadia-ANT+RF-test.nc`) to validate its metadata.

## Overview

The netCDF file inspector is a Python script that examines the following aspects of a NetCDF file:

- File type and size
- Dimensions and their sizes
- Coordinate variables (both primary and auxiliary)
- Latitude and longitude ranges
- Geospatial attributes
- Required and optional global attributes
- CF (Climate and Forecast) compliance
- Variables (model and coordinate) along with their attributes

## Step 1: Navigate to the model directory

Change your directory to the location of the model file:

```
cd sample-files/Cascadia-ANT+RF-Delph2018
```

Make sure the corresponding netCDF file exists (`Cascadia-ANT+RF-test.nc`).

2. **Run the cvm_inspector tool**

The tool will prompt you to input the netCDF file path to check:

```
 ../../src/cvm_inspector.py
 Please enter the file name:

```

Enter the file name and the inspector start checking the file's metadata.

```
Please enter the file name: Cascadia-ANT+RF-test.nc
```

### Step 2.1 Check the netCDF file's info

This section provides basic details about the file, such as:

- **File Path**: The location of the file on your machine.
- **File Size**: The size of the file in megabytes.
- **File Type**: The type of NetCDF file, which should be ` NetCDF-4 Classic Model`

### Step 2.2 Check the Metadata Inspection Report

A comprehensive summary of the metadata is provided here, including:

- **Dimensions and Sizes**: A list of dimensions and their sizes.
- **Coordinate Information**: Lists both primary and auxiliary coordinates. It also identifies the third dimension if applicable.
- **Latitude and Longitude Value Check**: Validates the range of latitude and longitude values.
- **Geospatial Attributes Check**: Ensures geospatial attributes such as `geospatial_lat_min`, `geospatial_lon_max`, etc., are present and correct.
- **Global Attributes Check**: Verifies the presence of required and optional global attributes.
- **CF Compliance Check**: Uses the `cfchecks` tool to assess whether the file complies with CF conventions.
- **Variables Summary**: Lists all variables, distinguishing between coordinate variables and model variables. For each variable, the script provides the range of values, units, and dimensions.

## Example Output

Example output for a NetCDF-4 file:

```
=== Dimensions and Sizes ===

- depth: 84 ✔️
- latitude: 46 ✔️
- longitude: 25 ✔️

=== Coordinate Information ===

Primary Coordinates: depth, latitude, longitude ✔️
Third Dimension: depth ✔️
Auxiliary Coordinates: easting, northing ✔️

=== Latitude and Longitude Value Check ===

Longitude Format: -180/180 degrees ✔️
Latitude Range: 40.000 to 49.000 ✔️
Longitude Range: -124.800 to -120.000 ✔️

=== Geospatial Attributes Check ===

geospatial_lat_min: Metadata = 40.0, Computed = 40.000 ✔️
geospatial_lat_max: Metadata = 49.0, Computed = 49.000 ✔️
geospatial_lon_min: Metadata = -124.8, Computed = -124.800 ✔️
geospatial_lon_max: Metadata = -120.0, Computed = -120.000 ✔️
geospatial_vertical_min: Metadata = -3.0, Computed = -3.000 ✔️
geospatial_vertical_max: Metadata = 80.0, Computed = 80.000 ✔️

=== Global Attributes Check ===

All required global attributes are present. ✔️
All optional global attributes are present. ✔️

=== CF Compliance Check ===

CF Compliance: Compliant ✔️

=== Variables Summary ===

Variable 'vs' has correct dimension order: depth, latitude, longitude. ✔️
Coordinate Variables:
  - depth: Range = -3.000 to 80.000, Units = km, Dimensions = depth ✔️
  - latitude: Range = 40.000 to 49.000, Units = degrees_north, Dimensions = latitude ✔️
  - longitude: Range = -124.800 to -120.000, Units = degrees_east, Dimensions = longitude ✔️
  - easting: Range = 346348.097 to 756099.648, Units = m, Dimensions = latitude, longitude ✔️
  - northing: Range = 4427757.219 to 5431792.865, Units = m, Dimensions = latitude, longitude ✔️
Model Variables:
  - vs: Range = 1.017 to 5.861, Units = km.s-1, Dimensions = depth, latitude, longitude ✔️

=== Metadata Inspection Summary ===

File Type: NetCDF-4
Dimensions:
  - depth: 84
  - latitude: 46
  - longitude: 25
Primary Coordinates: ['depth', 'latitude', 'longitude']
Auxiliary Coordinates: ['easting', 'northing']
Third Dimension: depth
Longitude Format: -180/180 degrees
Latitude Range: 40.000 to 49.000
Longitude Range: -124.800 to -120.000
CF Compliance: Compliant
Coordinate Variables:
  - depth: {'Range': '-3.000 to 80.000', 'Units': 'km', 'Dimensions': 'depth'}
  - latitude: {'Range': '40.000 to 49.000', 'Units': 'degrees_north', 'Dimensions': 'latitude'}
  - longitude: {'Range': '-124.800 to -120.000', 'Units': 'degrees_east', 'Dimensions': 'longitude'}
  - easting: {'Range': '346348.097 to 756099.648', 'Units': 'm', 'Dimensions': 'latitude, longitude'}
  - northing: {'Range': '4427757.219 to 5431792.865', 'Units': 'm', 'Dimensions': 'latitude, longitude'}
Model Variables:
  - vs: {'Range': '1.017 to 5.861', 'Units': 'km.s-1', 'Dimensions': 'depth, latitude, longitude'}


```

## Error Handling

If there are any errors during the file inspection process, the script will print the corresponding error message. These errors can be related to:

- File access issues
- Missing global or geospatial attributes
- CF compliance failures
- Incorrect dimension orders for variables

## Conclusion

This script is useful for ensuring that netCDF files adhere to required metadata standards and contain well-structured coordinate and variable data. It can also help diagnose issues with file structure, attributes, and compliance with CF conventions.

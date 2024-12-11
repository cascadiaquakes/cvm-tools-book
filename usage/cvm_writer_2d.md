# cvm_writer 2D

In this tutorial, we will use the `cvm_writer` tool to convert the raw 2D data (latitude, and longitude coordinates) for the `McCroryetal-2012` model into netCDF. These data are from <a href="https://doi.org/10.1029/2012JB009407" target="_blank">McCrory et al.</a> that represent depth to the Juan de Fuca slab beneath the Cascadia subduction margin.

To achieve this, we need:

- The model data in CSV format
- A global parameter file
- A parameter file for the variables

The parameter files are based on the templates from the `template` directory.

## Step 1: Navigate to the Model Directory

Change your directory to the model directory:

```
cd sample-files/McCroryetal-2012
```

## Step 2: Check the Data File

The `McCroryetal-2012_data.txt` file is the raw data file for the model. Look at the first line in the file that contains the column headers:

```
longitude latitude depth
```

**Note**: Unlike the 3D models, in this 2D data file **depth** is a data column and not a coordinate column.

## Step 3: Prepare the Metadata File

Now, we need model metadata files. These files are similar to the corresponding ones for the 3D models. The metadata files contain the model metadata as text. Templates for the metadata files are the same as the templates for the 3D models and are available under the `template` folder. Two metadata files are needed: one global based on `template/global_metadata_template.txt` and another for variables based on `template/variables_metadata_template.txt`.

For this tutorial, you do not need to copy templates. We already have the necessary metadata file for the global attributes as `McCroryetal-2012_global.txt` and for variables as `McCroryetal-2012_meta.txt` placed under this directory.

For detailed instructions on how to create these parameter files, see the **Parameter File Structure guide**. However, since we are dealing with a 2D mode, the following must be considered:

- The global attributes (`McCroryetal-2012_global.txt`) follow the same procedure as 3D models.
- The model attributes (`McCroryetal-2012_meta.txt`) require the following changes:

First, the model contains only longitude and latitude coordinates (x and y) and as such the definition for the z coordinate must be removed or commented out:

```
#> z
#    column =
#    variable = depth
#    positive = down
#    standard_name = depth
#    long_name = depth below sea level
#    units = km
```

Second, in this model, **depth** represent the model variable and therefore must be defined in the model variable section:

```
> variables
    >> depth
        column = depth
        variable = depth
        dimensions = 2
        long_name = Slab depth
        display_name = Slab depth (km)
        grid_ref = latitude_longitude
        units = km
        data_source = data-derived

```

## Step 4: (Optional) Convert Metadata to GeoCSV and JSON

This step is optional. Its purpose is to familiarize you with various metadata formats. During regular model format conversion, you can skip this step and go directly to Step 5.

Convert the metadata to GeoCSV by running the `cvm_writer.py` tool:

```
python ../../src/cvm_writer.py -m McCroryetal-2012_meta.txt -g McCroryetal-2012_global.txt -o McCroryetal-2012 -t metadata
```

- `-m McCroryetal-2012_meta.txt` tells `cvm_writer` that the variables metadata file is `McCroryetal-2012_meta.txt`.
- `-g McCroryetal-2012_global.txt` tells `cvm_writer` that the global metadata file is `McCroryetal-2012_global.txt`.
- `-o McCroryetal-2012` specifies the output filename prefix. For metadata, a postfix of `_metadata` will be added to the filename.
- `-t metadata` tells the code that we only want the metadata files.

After running this command, you should see two new files in your model directory:

- `McCroryetal-2012_metadata.csv` — the metadata file in GeoCSV format
- `McCroryetal-2012_metadata.json` — the metadata file in JSON format

## Step 5: Create the Model File

Now, create the model file by running:

```
python ../../src/cvm_writer.py -m McCroryetal-2012_meta.txt -g McCroryetal-2012_global.txt -o McCroryetal-2012 -d McCroryetal-2012_data.txt -t netcdf
```

- `-m McCroryetal-2012_meta.txt` tells `cvm_writer` that the variables metadata file is `McCroryetal-2012_meta.txt`.
- `-g McCroryetal-2012_global.txt` tells `cvm_writer` that the global metadata file is `McCroryetal-2012_global.txt`.
- `-o McCroryetal-2012` specifies the output filename prefix. For metadata, a postfix of `_metadata` will be added to the filename.
- `-d McCroryetal-2012_data.txt` tells the code where it can find the model data.
- `-t netcdf` specifies that we want the output to be in netCDF format.

After running this command, you should see a new file `McCroryetal-2012.nc`, which is our model in netCDF.

Please note that you could also use `-t geocsv` for GeoCSV output or combine them with `-t metadata,netcdf,geocsv` to get all the outputs.

## Step 6: (Optional) Examine the Output Files

If you created GeoCSV or JSON metadata files in step 4 above, look at these files to familiarize yourself with these formats.

## Step 7: Examine the netCDF File Content

To examine the netCDF file content, use the `netcdf_summary_info.py` script to summarize the created netCDF file. Upon execution, the script will prompt you for the name of the netCDF file to summarize. It will then read the netCDF file and provide a summary of the metadata and data contained in the file. Successful execution of this step indicates that the general structure of the netCDF file is correct and allows you to examine the data and metadata contained in the file to verify.

Run the following command:

```
python ../../src/netcdf_summary_info.py

Enter the path to the netCDF file: McCroryetal-2012.nc
```

After providing the file name, you will see a summary of the netCDF file content.

```
Summary of netCDF file: McCroryetal-2012.nc

Global Attributes:

- model: McCroryetal-2012
- id: McCroryetal-2012
- title: JdF slab geometry beneath the Cascadia subduction margin.
- summary: JdF slab geometry beneath the Cascadia subduction margin.
- reference: McCrory, Blair, Waldhauser, and Oppenheimer (2012)
- reference_pid: doi:10.1029/2012JB009407
- data_revision: r0.0
- version: v0.0
- Conventions: CF-1.0
- Metadata_Conventions: Unidata Dataset Discovery v1.0
- author_name: Patricia A. McCrory
- author_email:
- author_institution:
- author_url:
- repository_name: EMC
- repository_institution: EarthScope
- repository_pid: doi:
- geospatial_lon_min: -128.5
- geospatial_lon_max: -120.5
  ...
```

## Step 8: Validate the netCDF File Metadata

To examine the netCDF file content, use the `cvm_inspector.py` tool to check the metadata, dimensions, coordinates, and variables of a netCDF file. The tool provides a comprehensive inspection of the file and ensures compliance with the CF convention (see <a href="cvm_inspector.html">cvm_inspector tool</a>).

The tool will prompt you to input the netCDF file path to check:

```
../../src/cvm_inspector.py

Please enter the file name: McCroryetal-2012.nc

=== netCDF File Check ===
File: McCroryetal-2012.nc
Size: 5.99 MB
File Type: Unknown

=== Dimensions and Sizes ===

- latitude: 651 ✔️
- longitude: 401 ✔️

=== Coordinate Information ===

Primary Coordinates: latitude, longitude ✔️
Auxiliary Coordinates: easting, northing ✔️

=== Latitude and Longitude Value Check ===

Longitude Format: -180/180 degrees ✔️
Latitude Range: 39.000 to 52.000 ✔️
Longitude Range: -128.500 to -120.500 ✔️

=== Geospatial Attributes Check ===

geospatial_lat_min: Metadata = 39.0, Computed = 39.000 ✔️
geospatial_lat_max: Metadata = 52.0, Computed = 52.000 ✔️
geospatial_lon_min: Metadata = -128.5, Computed = -128.500 ✔️
geospatial_lon_max: Metadata = -120.5, Computed = -120.500 ✔️
geospatial_vertical_min: Not applicable (No depth dimension) ⚠️
geospatial_vertical_max: Not applicable (No depth dimension) ⚠️

=== Global Attributes Check ===

All required global attributes are present. ✔️
All optional global attributes are present. ✔️

=== CF Compliance Check ===

CF Compliance: Compliant ✔️

=== Variables Summary ===

Coordinate Variables:
  - easting: Range = 23592.286 to 716493.818, Units = m, Dimensions = latitude, longitude ✔️
  - northing: Range = 4316776.583 to 5775332.946, Units = m, Dimensions = latitude, longitude ✔️
  - latitude: Range = 39.000 to 52.000, Units = degrees_north, Dimensions = latitude ✔️
  - longitude: Range = -128.500 to -120.500, Units = degrees_east, Dimensions = longitude ✔️
Model Variables:
  - depth: Range = 4.992 to 100.176, Units = km, Dimensions = latitude, longitude ✔️

=== Metadata Inspection Summary ===

File Type: Unknown
Dimensions:
  - latitude: 651
  - longitude: 401
Primary Coordinates: ['latitude', 'longitude']
Auxiliary Coordinates: ['easting', 'northing']
Longitude Format: -180/180 degrees
Latitude Range: 39.000 to 52.000
Longitude Range: -128.500 to -120.500
CF Compliance: Compliant
Coordinate Variables:
  - easting: {'Range': '23592.286 to 716493.818', 'Units': 'm', 'Dimensions': 'latitude, longitude'}
  - northing: {'Range': '4316776.583 to 5775332.946', 'Units': 'm', 'Dimensions': 'latitude, longitude'}
  - latitude: {'Range': '39.000 to 52.000', 'Units': 'degrees_north', 'Dimensions': 'latitude'}
  - longitude: {'Range': '-128.500 to -120.500', 'Units': 'degrees_east', 'Dimensions': 'longitude'}
Model Variables:
  - depth: {'Range': '4.992 to 100.176', 'Units': 'km', 'Dimensions': 'latitude, longitude'}

```

## Step 9: Visualize Your New 2D netCDF to Ensure the Proper File Conversion

By going through this tutorial, we have created a 2D netCDF file (`McCroryetal-2012.nc`). Use the <a href="cvm_slicer.html">cvm_slicer tool</a> to create surface plots from this file and extract data from it to ensure it is properly converted from your original data files.

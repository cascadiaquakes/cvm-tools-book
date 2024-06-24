
# netcdf_to_geocsv

## Overview

The `netcdf_to_geocsv` tool is a utility tool for converting a netCDF CVM file to the corresponding CSV, GeoCSV format and optionally output its JSON metadata.

In this tutorial, we will demonstrate how to convert the `Cascadia-ANT+RF-test.nc` file to GeoCSV format and generate its metadata in JSON.

## Steps

1. **Navigate to the Model Directory**

   Change your directory to the location of the model file:

   ```bash
   cd sample-files/Cascadia-ANT+RF-Delph2018
   ```

2. **Run the netcdf_to_geocsv Script**

   Use the following command to convert the `Cascadia-ANT+RF-test.nc` file to GeoCSV and output its metadata in JSON:

   ```bash
   ../../src/netcdf_to_geocsv.py -i Cascadia-ANT+RF-test.nc -c true -g true -m true
   ```

**Command Breakdown**

- `-i Cascadia-ANT+RF-test.nc` : Specifies the name of the input file to convert.
- `-c true` : Sets the CSV conversion flag to True.
- `-g true` : Sets the GeoCSV conversion flag to True.
- `-m true` : Sets the JSON metadata output flag to True.

**Note**: You may set any of the above options to `false` to disable that option.

**Note:** The output files will have the same name as the input file but with `.csv` and `.json` extensions for the model file and metadata file respectively. If both CSV and GeoCSV files are requested, the GeoCSV file's extension will be `.gcsv`.

## Output Files

By running the command, the tool will generate three files:

- `Cascadia-ANT+RF-test.gcsv` : The converted GeoCSV file.
- `Cascadia-ANT+RF-test.csv` : The converted CSV file.
- `Cascadia-ANT+RF-test.json` : The metadata in JSON format.

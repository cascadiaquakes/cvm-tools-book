# netcdf_to_cvm

## Overview

The `netcdf_to_cvm` tool is a utility tool for converting an existing netCDF CVM file to the corresponding CVM-compliant netCDF file. This tool will add any missing CVM attributes based on the provided metadata files.

In this tutorial, we will demonstrate how to run `netcdf_to_cvm` on a CVM netCDF file `Cascadia-ANT+RF-test-missing.nc` that is missing some CVM metadata attributes.

## Steps

1. **Navigate to the model directory**

   Change your directory to the location of the model file:

   ```
   cd sample-files/Cascadia-ANT+RF-Delph2018
   ```

2. **Update the parameter files**

   To create a netCDF file with some missing attributes, edit the global file and comment out the `data_layout` attribute in `Cascadia-ANT+RF_global_meta.txt` file:

   `# data_layout = vertex`

   also edit the variables parameter file `Cascadia-ANT+RF_meta.txt` and comment out the `data_source` attribute:

   `#  data_source = data-derived`

3. **Create a netCDF file with missing attributes**

   We create `Cascadia-ANT+RF-test-missing.nc` the same way we created `Cascadia-ANT+RF-test` in our **cvm_writer** tutorial. The only difference is that each parameter file has a missing attribute and we want to output the file to `Cascadia-ANT+RF-test-missing.nc`

   ```

   python ../../src/cvm_writer.py -m Cascadia-ANT+RF_meta.txt -g Cascadia-ANT+RF_global_meta.txt -o Cascadia-ANT+RF-test-missing -d Cascadia-ANT+RF_data.txt -t netcdf

   ```

   Check and verify that `Cascadia-ANT+RF-test-missing.nc` is created.

4. **Run the netcdf_to_cvm tool**

   Before we run the `netcdf_to_cvm` tool to detect and correct the missing parameters, we need to update the `Cascadia-ANT+RF_global_meta.txt` and `Cascadia-ANT+RF_meta.txt` and uncomment the parameters we commented in step 2 above:

   ```

   data_source = data-derived
   data_layout = vertex

   ```

   Now, use the **netcdf_to_cvm** tool to update the `Cascadia-ANT+RF-test-missing.nc` file and add the missing parameters to it and save the updated model as `Cascadia-ANT+RF-test-updated`:

   ```

   ../../src/netcdf_to_cvm.py -d Cascadia-ANT+RF-test-missing.nc -g Cascadia-ANT+RF_global_meta.txt -m Cascadia-ANT+RF_meta.txt -o Cascadia-ANT+RF-test-updated

   ```

   **Command breakdown**

   - `-d Cascadia-ANT+RF-test-missing.nc`: Specifies the name of the input file to check.
   - `-g Cascadia-ANT+RF_global_meta.txt`: Specifies the global metadata file.
   - `-m Cascadia-ANT+RF_meta.txt`: Specifies the variables metadata file.
   - `-o Cascadia-ANT+RF-test-updated.nc`: Specifies the name of the output file (**do not include a file extension**).

   The `netcdf_to_cvm` output, as shown below, informs us of what it needed to update/add in the file:

   ```

   [INFO] Cascadia-ANT+RF-test-missing.nc is a netCDF file
   [INFO] nc_format: '{'format': 'NETCDF4_CLASSIC', 'encoding': {'zlib': True, 'complevel': 9}}'
   [INFO] Added the missing global attribute data_layout: 'vertex'
   [INFO] Added the missing vs attribute data_source: 'data-derived'
   [Elapsed time: 3.14s] Model netCDF file: Cascadia-ANT+RF-test-updated.nc

   ```

5. **Verification**

   Use the **netCDF_summary_info** utility tool to verify that the listed updates have taken place.

   ```

   ../../src/netCDF_summary_info.py
   Enter the path to the netCDF file:

   ```

   For example:

   **From `Cascadia-ANT+RF-test-missing.nc` summary output**:

   ```

   Global Attributes:

   - title: 3D vertical shear-wave velocity model of the Cascadian forearc from the joint inversion of ambient noise dispersion and receiver functions
   - institution: Rice University
   - source: Cascadia-ANT+RF-Delph2018
   - history: Created on 2023-05-01
   - references: Delph, J.R., Levander, A., Niu, F. (2018)
   - conventions: CF-1.6

   Dimensions:

   - depth: 84
   - latitude: 46
   - longitude: 25

   Variables:

   - depth (dimensions: ('depth',), shape: (84,))
     - units: km
     - long_name: Depth below sea level
       Range: -3.00 to 80.00
   - latitude (dimensions: ('latitude',), shape: (46,))
     - units: degrees_north
     - long_name: Latitude
       Range: 40.00 to 49.00
   - longitude (dimensions: ('longitude',), shape: (25,))
     - units: degrees_east
     - long_name: Longitude
       Range: -124.80 to -120.00
   - vs (dimensions: ('depth', 'latitude', 'longitude'), shape: (84, 46, 25))
     - units: km/s
     - long_name: Shear-wave velocity
       Range: 2.50 to 4.50

   ```

   **From `Cascadia-ANT+RF-test-updated.nc` summary output**:

   ```

   Global Attributes:

   - title: 3D vertical shear-wave velocity model of the Cascadian forearc from the joint inversion of ambient noise dispersion and receiver functions
   - institution: Rice University
   - source: Cascadia-ANT+RF-Delph2018
   - history: Created on 2023-05-01
   - references: Delph, J.R., Levander, A., Niu, F. (2018)
   - conventions: CF-1.6
   - data_layout: vertex

   Dimensions:

   - depth: 84
   - latitude: 46
   - longitude: 25

   Variables:

   - depth (dimensions: ('depth',), shape: (84,))
     - units: km
     - long_name: Depth below sea level
       Range: -3.00 to 80.00
   - latitude (dimensions: ('latitude',), shape: (46,))
     - units: degrees_north
     - long_name: Latitude
       Range: 40.00 to 49.00
   - longitude (dimensions: ('longitude',), shape: (25,))
     - units: degrees_east
     - long_name: Longitude
       Range: -124.80 to -120.00
   - vs (dimensions: ('depth', 'latitude', 'longitude'), shape: (84, 46, 25))
     - units: km/s
     - long_name: Shear-wave velocity
     - data_source: data-derived
       Range: 2.50 to 4.50

   ```

# show_file_structure

## Overview

The `show_file_structure.py` reads a file (either HDF5 or netCDF format) and prints its structure, including the file name, size, and type. It is useful for quickly inspecting the contents of the model data files.

## Usage

### Step 1: Navigate to the Model Directory

Change your directory to the model directory containing the files you want to check:

```sh
cd sample-files/Cascadia-ANT+RF-Delph2018
```

### Step 2: Run the Script:

Execute the script using Python:

```bash
python ../../src/show_file_structure.py
```

### Step 3: Provide the Input File's Name

**Example 1**: The file structure of an HDF5 file with a single group of datasets.:

`Enter the path to the input file (HDF5 or netCDF): Cascadia-ANT+RF-test.h5`

See the file structure. In this case we set the dataset_group to blanks, so the dataset is placed under the **MODEL** group:

```bash
File Name: Cascadia-ANT+RF-test.h5
File Size: 806936 bytes
File Type: HDF5

HDF5 File Structure:
├── MODEL
│   ├── depth
│   ├── easting
│   ├── latitude
│   ├── longitude
│   ├── northing
│   ├── vs
```

**Example 2**: The file structure of an HDF5 file with two subgroups of datasets:

`Enter the path to the input file (HDF5 or netCDF): Cascadia-ANT+RF-test_2.h5`

See the file structure. Each dataset appear under its own **dataset_group**:

```bash
File Name: Cascadia-ANT+RF-test_2.h5
File Size: 832920 bytes
File Type: HDF5

HDF5 File Structure:
├── MODEL
│   ├── depth_gt_40km
│   │   ├── depth
│   │   ├── easting
│   │   ├── latitude
│   │   ├── longitude
│   │   ├── northing
│   │   ├── vs
│   ├── depth_le_40km
│   │   ├── depth
│   │   ├── easting
│   │   ├── latitude
│   │   ├── longitude
│   │   ├── northing
│   │   ├── vs
```

**Example 3**: The file structure of a netCDF file:
`Enter the path to the input file (HDF5 or netCDF): Cascadia-ANT+RF-Delph2018.r0.1.nc`

See the file structure.

File Name: Cascadia-ANT+RF-Delph2018.r0.1.nc
File Size: 817194 bytes
File Type: netCDF

```bash
netCDF File Structure:
Dimensions:
├── depth: 84
├── latitude: 46
├── longitude: 25
Variables:
├── depth: ('depth',)
├── latitude: ('latitude',)
├── longitude: ('longitude',)
├── easting: ('latitude', 'longitude')
├── northing: ('latitude', 'longitude')
├── vs: ('depth', 'latitude', 'longitude')
```

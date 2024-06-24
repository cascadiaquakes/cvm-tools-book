
# hdf5_summary_info

## Overview

The `hdf5_summary_info.py` script is a utility designed to read, analyze, and provide a comprehensive summary of an HDF5 file's contents. This script outputs detailed information about groups, datasets, attributes, and data ranges within the HDF5 file, helping users to verify the overall structure and integrity of the file.

## Script Usage

1. **Running the Script**:

   - Run the script using Python:
     ```sh
     src/hdf5_summary_info.py
     ```

2. **Input File Path**:
   - When prompted, enter the path to the HDF5 file you want to summarize.

## Features

- **Global Attributes**:
  - Displays global attributes of the HDF5 file, providing context and metadata about the file.

- **Group Information**:
  - Lists all groups within the file, including group attributes.

- **Dataset Information**:
  - Lists all datasets within the file, including their shapes and data types.
  - Displays dataset-specific attributes.
  - Calculates and prints the range of values for each dataset, formatted to two decimal places.

## Example Output

Running the script with a sample HDF5 file might produce output like this:

```
Group: surfaces

Group: surfaces/srtm_elevation

Dataset: surfaces/srtm_elevation/easting (shape: (40, 50), dtype: float64)
  - Attribute long_name: easting; UTM
  - Attribute standard_name: projection_y_coordinate
  - Attribute units: m
  Range: 271930.43 to 644446.78

Dataset: surfaces/srtm_elevation/elevation (shape: (40, 50), dtype: float64)
  - Attribute DIMENSION_LIST: [array([<HDF5 object reference>], dtype=object)
 array([<HDF5 object reference>], dtype=object)]
  - Attribute coordinates: easting northing
  - Attribute display_name: Elevation above sea level (m)
  - Attribute grid_mapping: latitude_longitude
  - Attribute long_name: Elevation above sea level
  - Attribute standard_name: surface_altitude
  - Attribute units: m
  Range: nan to nan

Dataset: surfaces/srtm_elevation/latitude (shape: (40,), dtype: float64)
  - Attribute CLASS: b'DIMENSION_SCALE'
  - Attribute REFERENCE_LIST: [(<HDF5 object reference>, 0)]
  - Attribute long_name: Latitude; positive north
  - Attribute standard_name: latitude
  - Attribute units: degrees_north
  Range: 47.00 to 50.90
```

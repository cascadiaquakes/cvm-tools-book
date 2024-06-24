
# netcdf_summary_info

## Overview

The `netcdf_summary_info.py` script is a utility designed to read, analyze, and provide a comprehensive summary of a netCDF4 classic file's contents. This script outputs detailed information about dimensions, variables, attributes, and data ranges within the netCDF file, helping users to verify the overall structure and integrity of the file.

## Script Usage

1. **Running the Script**:

   - Run the script using Python:
     ```sh
     src/netcdf_summary_info.py
     ```

2. **Input File Path**:
   - When prompted, enter the path to the netCDF file you want to summarize.

## Features

- **Global Attributes**:
  - Displays global attributes of the netCDF file, providing context and metadata about the file.

- **Dimensions Information**:
  - Lists all dimensions in the file along with their sizes, giving an overview of the data structure.

- **Variables Summary**:
  - Lists all variables in the file along with their dimensions and shapes.
  - Displays attributes specific to each variable, such as units and long names.
  - Calculates and prints the range of values for each variable, formatted to two decimal places.

## Example Output

Running the script with a sample netCDF file might produce output like this:

```
Global Attributes:
  - model: SVI_EQTOMO_Savard2018
  - id: SVI_EQTOMO_Savard2018
  - title: Southern Vancouver Island double difference
  - summary: Double difference tomography from inversion of earthquake and low-frequency earthquake travel times on Southern Vancouver Island.
  - reference: Savard, Bostock, and Christensen (2018)
  - reference_pid: doi.org/10.1029/2017GC007417
  - data_revision:
  - version: v0.0
  - Conventions: CF-1.0
  - Metadata_Conventions: Unidata Dataset Discovery v1.0
  - author_name: Michael Bostock
```

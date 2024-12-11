# convert_to_csv_2d

## Overview

The `convert_to_csv_2d` tool is a utility script for converting 2D netCDF or GeoJSON files to a CSV format. It extracts the essential coordinate data (`x`, `y`) and includes any associated metadata or attributes.

In this tutorial, we assume yu want to convert a 2D netCDF file (`example.nc`) or GeoJSON file (`example.geojson`) from the `/sample_files/2d` directory to a CSV file.

## Steps

### 1. **Navigate to the File Directory**

Change your directory to the location of the 2D netCDF or GeoJSON files:

```bash
cd sample_files/2d
```

### 2. **Run the `convert_to_csv_2d` Script**

Use the `convert_to_csv_2d` script to convert the `example.nc` or `example.geojson` file to CSV format:

#### For a netCDF File:

```bash
../../src/convert_to_csv_2d.py -i example.nc -o example.csv
```

#### For a GeoJSON File:

```bash
../../src/convert_to_csv_2d.py -i example.geojson -o example.csv
```

### Command Breakdown

- `-i example.nc` or `-i example.geojson`: Specifies the name of the input file to convert.
- `-o example.csv`: Specifies the name of the output CSV file.

**Note:** The output file will contain coordinate columns (`x`, `y`) and any additional metadata or attributes from the original file.

### 3. **Verify the Output Files**

After running the script, you should see the corresponding CSV file in the same directory as your input file.

## Example Outputs

### Input GeoJSON File

#### Input: `example.geojson`

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": { "name": "Feature1", "value": 10 },
      "geometry": {
        "type": "Point",
        "coordinates": [102.0, 0.5]
      }
    },
    {
      "type": "Feature",
      "properties": { "name": "Feature2", "value": 20 },
      "geometry": {
        "type": "LineString",
        "coordinates": [
          [103.0, 1.0],
          [104.0, 2.0]
        ]
      }
    }
  ]
}
```

#### Output CSV File

#### Output: `example.csv`

```csv
name,value,x,y
Feature1,10,102.0,0.5
Feature2,20,103.0,1.0
Feature2,20,104.0,2.0
```

### Input netCDF File

#### Input: `example.nc`

The netCDF file `example.nc` is assumed to contain 2D data variables (`x`, `y`) along with associated attributes or metadata.

#### Output CSV File

#### Output: `example.csv`

```csv
x,y,temperature,pressure
102.0,0.5,25.6,1013.2
103.0,1.0,26.1,1012.8
104.0,2.0,27.0,1011.5
```

## Notes

1. **Handling Missing Values**:

   - Any missing values in the input file are represented as `NaN` in the output CSV.

2. **Supported Geometry Types (GeoJSON)**:

   - The script supports `Point` and `LineString` geometry types.
   - For multi-point geometries like `LineString`, each point is represented as a separate row in the CSV.

3. **netCDF Data Extraction**:

   - The script extracts coordinate data (`x`, `y`) and all 2D attributes or variables in the netCDF file.

4. **Flexibility**:

   - The script dynamically detects the file type (netCDF or GeoJSON) without relying on file extensions.

5. **Output Columns**:
   - GeoJSON: Includes properties (`name`, `value`, etc.) and coordinates (`x`, `y`).
   - netCDF: Includes variables and their respective coordinate data (`x`, `y`).

## Troubleshooting

- Ensure that the input file is a valid 2D netCDF or GeoJSON file.
- Check that the `/sample_files/2d` directory contains the file you want to convert.
- If encountering issues, run the script with the `-h` option to display the help message:
  ```bash
  ../../src/convert_to_csv_2d.py -h
  ```

This guide ensures that you can seamlessly convert 2D netCDF and GeoJSON files to CSV format. For further assistance, feel free to consult the script documentation.

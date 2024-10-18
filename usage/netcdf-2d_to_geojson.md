# netcdf-2d_to_geojson

This tool converts 2D netCDF (.nc) or .grd files into GeoJSON format, supporting rectangular and triangular grid representations. It can handle depth or elevation variables and allows decimation of data to improve performance.

## Features

- Converts 2D netCDF/GRD files into GeoJSON format.
- Supports both **rectangular** and **triangular** grid representations.
- Option to **minify** the GeoJSON file to reduce size.
- Handles **depth or elevation** in kilometers or meters.
- Allows **decimation** of data to reduce complexity.

## Usage

### 1. Run the Script

To use the script, you will be prompted for the necessary inputs:

```bash
python netcdf-2d_to_geojson.py
```

### 2. Input Parameters

The script will ask for the following inputs:

1. **Input File**: Path to the netCDF or .grd file.

   - Example: `input.nc`

2. **Output File**: Path where the resulting GeoJSON file will be saved.

   - Example: `output.geojson`

3. **Latitude Variable**: The name of the latitude variable in the netCDF file.

   - Example: `latitude`

4. **Longitude Variable**: The name of the longitude variable in the netCDF file.

   - Example: `longitude`

5. **Depth/Elevation Variable**: The name of the depth or elevation variable in the file.

   - Example: `depth`

6. **Depth Unit**: The unit of depth. You can choose between kilometers (`km`) or meters (`m`).

   - Example: `km`

7. **Decimation Factor**: The factor by which data should be decimated (i.e., reduce the number of points).

   - Example: `2` (will take every second point)

8. **Grid Type**: Select the grid type, either `rectangular` or `triangular`.

   - Example: `rectangular`

9. **Minify Option**: Choose whether to minify the GeoJSON file to reduce its size. Enter `yes` or `no`.
   - Example: `yes`

### 3. Example Interaction

Here’s an example of how the script may prompt you:

```bash
cd sample-files/McCroryetal-2012
python ../../src/netcdf-2d_to_geojson.py

2D netCDF/.grd file to GeoJSON Converter!

Enter the path to the input NetCDF/GRD file [default: input.nc]: McCroryetal-2012.nc
Enter the path to save the GeoJSON output [default: output.geojson]: McCroryetal-2012.geojson
Enter the name of the latitude variable [default: latitude]: lat
Enter the name of the longitude variable [default: longitude]: lon
Enter the name of the depth/elevation variable [default: depth]: depth
Enter the depth unit [km / m] (default: km): km
Enter the decimation factor (integer) (default: 2): 5
Enter the grid type [rectangular / triangular] (default: rectangular): rectangular
Do you want to minify the GeoJSON file? [yes / no] (default: no): yes
```

### 4. Output

The script generates a GeoJSON file in the location specified by the user, containing a surface representation of the data from the netCDF or .grd file. The file can be imported into visualization tools like CesiumJS for further analysis.

### 5. Error Handling

The script validates:

- If the input file exists.
- If the variable names (latitude, longitude, depth/elevation) are correct.
- That valid grid types and decimation factors are provided.

If any error occurs, a message will be displayed, and you can correct your input.

### 6. Example Script Call

Here’s how to call the function directly in Python with specific parameters:

```python
grd_to_geojson_surface(
    input_file="McCroryetal-2012.nc",
    output_file="McCroryetal-2012.geojson",
    lat_var="lat",
    lon_var="lon",
    z_var="depth",
    depth_unit="km",
    minify=True,
    decimation_factor=5,
    grid_type="rectangular"
)
```

## FAQ

### 1. What is decimation, and why would I use it?

**Decimation** reduces the number of data points used from the original dataset. This can help improve performance when working with large datasets by reducing the complexity of the resulting GeoJSON file.

### 2. What does "minify" mean?

**Minifying** a file removes unnecessary whitespace and line breaks, making the file smaller but harder to read. This is useful when you need a compact file size for web applications.

### 3. What is the difference between rectangular and triangular grids?

- **Rectangular grids**: Each data cell is represented as a rectangle.
- **Triangular grids**: Each rectangle is split into two triangles, which can provide a more detailed surface representation.

## Troubleshooting

If the script throws an error, check the following:

- Ensure that the input file path is correct.
- Verify the variable names in the netCDF/GRD file.
- Use a valid grid type (`rectangular` or `triangular`).

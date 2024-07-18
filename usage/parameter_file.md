# Parameter File Structure

When converting model data to netCDF or HDF5, it is essential to provide detailed model metadata. In this guide, we will explore how to construct metadata using parameter files. These parameter files follow specific rules and conventions, ensuring consistency and compliance with the CF Metadata Conventions.

## Overview

Parameter files define various model parameters used to construct metadata. All parameters must adhere to the CF Metadata Conventions, which can be found [here](https://cfconventions.org/).

## General Rules

1. **Comments and Blank Lines**:

   - Lines starting with `#` are comments and are ignored.
   - Blank lines are ignored.
   - Leading and trailing blank spaces are ignored.

2. **Parameter Definitions**:

   - Each parameter should be defined on a new line using the `key=value` format.
   - Quotes are not required for the values and should not be included.

3. **Grouping and Sub-grouping**:
   - Lines starting with `-` indicate a new parameter definition.
   - Lines starting with `>` indicate a new parameter group.
   - Each parameter group should contain one or more parameter definitions.
   - Lines starting with `>>` indicate a new parameter sub-group. Each parameter group (>) may contain as many subgroups (>>) as necessary.
   - Each parameter sub-group should be nested under a parameter group.
   - Each parameter sub-group should contain one or more parameter definitions.

## Types of Metadata

There are two types of model metadata. The global metadata that apply to the entire model, and variable metadata that are defined for individual variables (coordinate and data variables). To manage this grouping effectively, we place these metadata into **two separate files**.

### Global Metadata

The global metadata apply to the entire model. You will find a template file for the global metadata under the template directory (`template/global_metadata_template.txt`). The global metadata includes:

#### Delimiters

Define the delimiters that are used to separate data columns in both input and output files. The value assigned to **data** represents the characters that separates columns in your data file. If your file is space-delimited, leave the **data** value blank. The **geocsv** represents the delimiter to use to separate the GeoCSV data columns.

```
> delimiter
    data =
    geocsv = |
```

#### HDF5 Groups

These attributes applies to the HDF5 files only and will be ignored by netCDF. By default, the model values and other 3D data are stored as uniform grids within the **volumes** group. The elevation of surfaces or other 2D data are stored within the **surfaces** group.

```
> groups
     volumes = volumes
     surfaces = surfaces
```

#### netCDF Output Format

Specify the netCDF format to use, as defined in `prop/shared_prop.py`.

```
- netcdf_format = NETCDF4C
```

#### Model Information

Provide details about the model, including its name, title, summary, and references.

```
> model
    model = Cascadia_ANT+RF_Delph2018
    title = 3D vertical shear-wave velocity model of the Cascadian forearc from the joint inversion of ambient noise dispersion and receiver functions
    summary = Cascadia_ANT+RF_Delph2018 was created from the joint inversion of ambient noise Rayleigh waves dispersion measurements (8-50 seconds) and adaptive CCP-derived receiver functions (see Delph et al., 2015, 2017 for details of methodology; Delph et al., 2018 for details of this model).
    reference = Delph, Levander, and Niu (2018)
    reference_pid = doi:10.1029/2018gl079518
    data_revision = r0.1
    version = v0.0
```

#### Repository Information

Include the persistent identifier for the model in the repository.

```
> repository
    repository_pid = doi:10.17611/dp/cascadiaantrfd2018
```

#### Corresponding Author

Provide details about the corresponding author.

```
> corresponding_author
    author_name = Jonathan R. Delph
    author_email = jdelph@purdue.edu
    author_institution = Purdue University
    author_url = https://www.eaps.purdue.edu/delph/
```

#### Geospatial Limits

Define the geographical area covered by the dataset.

```
> geospatial
    geospatial_lon_min = -124.8
    geospatial_lon_max = -120
    geospatial_lon_units = degrees_east
    geospatial_lon_resolution = 0.2
    geospatial_lat_min = 40
    geospatial_lat_max = 49
    geospatial_lat_units = degrees_north
    geospatial_lat_resolution = 1
    geospatial_vertical_min = -3
    geospatial_vertical_max = 80
    geospatial_vertical_units = km
    geospatial_vertical_positive = down
```

#### Global Attributes

Include additional parameters as global attributes.

```
> global_attrs
    keywords = seismic, Rayleigh waves dispersion, shear wave, s wave, Cascadian forearc, ambient noise dispersion, receiver functions
    acknowledgment = Model was provided by Jonathan R. Delph of Department of Earth, Environmental and Planetary Sciences, Rice University
    history = [2024-01-03] Converted to netCDF via CRESCENT data tools.
    comments = CRESCENT CVM tools development project.
    data_layout = vertex
```

##### data_layout attribute

Each model should also include a global attribute `data_layout`. This attribute specifies the layout of the data in the file and can take two possible values:

- `'vertex'` for vertex-based layout (values are specified at vertices)
- `'cell'` for cell-based layout (values are specified at the centers of grid cells)

Currently, the CVM-Tools support vertex-based values.

#### Grid Mapping

Specify a recognized grid mapping name. Must correspond to a recognized grid mapping name, ([more information](https://cfconventions.org/cf-conventions/cf-conventions.html#appendix-grid-mappings))

Currently supporting:

- **latitude_longitude** -- This grid mapping defines the canonical 2D geographical coordinate system based upon latitude and longitude coordinates.
- **mercator** -- Mercator

```
- grid_mapping_name = latitude_longitude
```

#### Universal Transverse Mercator (UTM) Zone

Define the UTM zone and ellipsoid reference.

```
- utm_zone = 10
- ellipsoid = WGS84
```

### Variables Metadata

Metadata for variables consist of attributes for individual variables, both coordinate variables and data variables. A template for variables metadata is available under the template directory (`template/variables_metadata_template.txt`). The variables metadata includes:

#### Dataset group

This parameter is required for HDF5 output files only and, if provided, will be used to create a subgroup under the root group for the dataset.

- An empty dataset_group is not allowed.
- Duplicate dataset_group names may result in variable conflicts and code failure.

```
- dataset_group = velocity
```

#### Primary Coordinates

Define the primary X, Y, and Z coordinates.

##### X Coordinate

```
> x
    column = longitude
    variable = longitude
    standard_name = longitude
    long_name = Longitude; positive east
    units = degrees_east
```

##### Y Coordinate

```
> y
    column = latitude
    variable = latitude
    long_name = Latitude; positive north
    units = degrees_north
    standard_name = latitude
```

##### Z Coordinate (if applicable). The z coordinate could be depth, for velocity models, period for phase velocity models, etc..

```
> z
    column = depth
    variable = depth
    positive = down
    standard_name = depth
    long_name = depth below sea level
    units = km
```

#### Auxiliary Coordinates

Define auxiliary X and Y coordinates, if necessary.

**NOTES**:

- Leave the column field EMPTY if you want the code to compute the auxiliary coordinate.
- The auxiliary X coordinate could be longitude for the geographic coordinate system, or easting for UTM projection.

##### Auxiliary X Coordinate

```
> x2
    column =
    variable = easting
    standard_name = easting
    long_name = easting; UTM
    units = m
```

##### Auxiliary Y Coordinate

```
> y2
    column = northing
    variable = northing
    long_name = northing; UTM
    units = m
    standard_name = northing
```

#### Variables

Define model variables, including column headers, variable names, and descriptions.

```
> variables
    >> vp
        column = vp
        variable = vp
        dimensions = 3
        long_name = P-wave velocity
        display_name = P Velocity (km/s)
        units = km.s-1
        source = data-derived
    >> vs
        column = vs
        variable = vs
        dimensions = 3
        long_name = Shear-wave velocity
        display_name = S Velocity (km/s)
        units = km.s-1
        source = vp/sqrt(3)
```

##### Source variable attribute

In addition to the standard CF variable attributes, each model variable should contain a `source` attribute that describes the origin of the data for this variable:

- If the data is derived from observations, the `source` attribute should be set to "data-derived."
- If the data is derived from an empirical formula, the `source` attribute should indicate how the variable was derived.

For example:

- `>> vp
source = data-derived`
- `>> vs
source = assumed to follow vp as vs = vp / 3`

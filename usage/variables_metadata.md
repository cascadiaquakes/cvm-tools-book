# Variable Metadata File Structure

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

## Metadata

There are two types of model metadata. The global metadata that apply to the entire model, and variable metadata that are defined for individual variables (coordinate and data variables). To manage this grouping effectively, we place these metadata into **two separate global and variable metadata files**. This guide describes the variables metadata structure.

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

**Note**: Make sure that `column` matches the corresponding variable in the first row of the data file!

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

**Notes**:

- Leave the column field EMPTY if you want the code to compute the auxiliary coordinate.
- The auxiliary X coordinate could be longitude for the geographic coordinate system, or easting for UTM projection.
- Make sure that `column` matches the corresponding variable in the first row of the data file!

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

A compilation of model variables metadata, including column headers, variable names, and descriptions.

**_Important_**: See the **Model Variable Naming and Unit Requirements** under the <a href="../standards_and_conventions.html" target="_blank">Standards and Conventions</a> for model name and unit rules.

Add a `>>` subgroup for as many variables as needed.

Each model variable metadata includes:

- column: The column heading in the data file:
- variable: the model variable name. It is recommended to use a CF-compliant standard name.
- long_name: Text that describes the variable more fully.
- display_name: Text to use for variable display.
- grid_ref: Text A recognized grid coordinate system (Currently supporting, latitude_longitude and mercator)
- data_source: describes the origin of the data for this variable:

      - If the data is derived from observations, the source attribute should be set to “data-derived.”
      - If the data is derived from an empirical formula, the source attribute should indicate how the variable was derived.

      For example:
           >> Vp
              data_source = data-derived
           >> Vs
              data_source = assumed to follow vp as Vs = Vp / 3

**Note**: Make sure that `column` values match the corresponding variables in the first row of the data file! The other parameters (e.g., variable, long_name, etc.) are customizable, as is the the name after `>>`

```
> variables
    >> Vp
        column = vp
        variable = Vp
        dimensions = 3
        long_name = P-wave velocity
        display_name = P Velocity (km/s)
        units = km.s-1
        source = data-derived
    >> Vs
        column = Vs
        variable = vs
        dimensions = 3
        long_name = Shear-wave velocity
        display_name = S Velocity (km/s)
        units = km.s-1
        source = vp/sqrt(3)
```

##### Source variable attribute

In addition to the standard CF variable attributes, each model variable should contain a `source` attribute that describes the origin of the data for this variable:

- If the data is derived from observations, the `source` attribute **should be set to** "data-derived."
- If the data is derived from an empirical formula, the `source` attribute should indicate how the variable was derived.

For example:

- `>> Vp
source = data-derived`
- `>> Vs
source = assumed to follow Vp as Vs = Vp / 3`

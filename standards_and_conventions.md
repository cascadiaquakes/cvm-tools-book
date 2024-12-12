# Standards and Conventions

The **Standards and Conventions** tutorial provides a comprehensive guide on the essential standards and conventions that CVM-Tools are based on. This tutorial covers the supported file formats, metadata requirements, and coordinate systems, ensuring that all users follow a uniform approach to creating, distributing, and utilizing CVM model files. By adhering to these conventions, researchers can enhance the consistency and interoperability of their models, facilitating more effective collaboration and data sharing. The tutorial also emphasizes the importance of metadata, detailing the necessary attributes and their formats, and provides guidelines for coordinate system usage to minimize distortion and improve accuracy. This foundational knowledge is crucial for maintaining the integrity and usability of the CVM data and tools.

## File Formats

The primary supported file formats for CVM files are [netCDF](https://www.unidata.ucar.edu/software/netcdf/) (Network Common Data Form) and [HDF5](https://www.hdfgroup.org/) (Hierarchical Data Format).

Using these formats for Earth models is particularly beneficial due to several key reasons:

### netCDF

1. **Self-Describing Nature**: netCDF files include metadata within the file itself, which describes the data's contents and structure. This makes it easier to understand and use the data without needing external documentation.
2. **Multi-Dimensional Arrays**: Earth models often involve complex, multi-dimensional data (e.g., 3D grids of seismic velocities). netCDF is specifically designed to handle such multi-dimensional data efficiently.
3. **Portability and Compatibility**: netCDF files are platform-independent and can be used across different operating systems and hardware configurations. They are widely supported by various scientific software and programming languages, including Python, MATLAB, and R.
4. **Efficient Data Access**: netCDF provides efficient data access, allowing for the retrieval of specific subsets of large datasets without needing to load the entire file into memory. This is crucial for handling large-scale Earth models.
5. **Standardized Format**: netCDF follows standardized conventions (e.g., CF Conventions), promoting consistency and interoperability between different datasets and tools within the geoscience community.

### HDF5

1. **Hierarchical Structure**: HDF5 supports a hierarchical structure, allowing data to be organized into groups and datasets. This is particularly useful for managing complex Earth models with multiple variables, resolutions, and auxiliary data.
2. **Scalability and Performance**: HDF5 is designed for high performance and can efficiently handle large datasets, making it suitable for storing detailed Earth model data. It supports various compression algorithms, reducing file size while maintaining quick access to the data.
3. **Flexibility**: HDF5 allows for flexible data organization and can store different types of data (e.g., integers, floats, strings) within a single file. This flexibility makes it ideal for Earth models that include diverse data types.
4. **Parallel I/O**: HDF5 supports parallel I/O operations, enabling faster read/write speeds when working with large datasets in high-performance computing environments. This is crucial for large-scale simulations and data processing tasks in Earth sciences.
5. **Rich Metadata**: Like netCDF , HDF5 allows extensive metadata to be embedded within the file, providing detailed information about the data's origin, structure, and meaning. This enhances data discoverability and usability.

Both netCDF and HDF5 provide robust, scalable, and efficient ways to store, manage, and share Earth model data. Their widespread adoption in the geosciences ensures compatibility with a wide range of analysis tools and platforms, facilitating collaboration and advancing our understanding of Earth's processes.

### Primary Formats

The primary formats for CVM models are netCDF and HDF5, and the CVM-Tools are built to support these formats.

| Format | Type             | Description                                                                                                                                                   |
| ------ | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| netCDF | netCDF 4 Classic | The netCDF 4 Classic provides the netCDF -4 performance benefits while using the classic data model. This format supports compression for smaller file sizes. |
| HDF5   | HDF5             | A versatile data model that can represent complex data objects and a wide variety of metadata.                                                                |

### Supported Formats for Data Extraction

In addition to the primary formats (netCDF and HDF5), the CVM-Tools also supports other formats, such as CSV, GeoCSV, SPECFEM, and GeoModelGrids, for data extraction output. Additional tools are provided to convert from the two primary formats to any of these supported formats.

| Format        | Type             | Description                                                                                                                                                                                                                                |
| ------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| netCDF        | netCDF 4 Classic | The netCDF 4 Classic provides the netCDF -4 performance benefits while using the classic data model. This format supports compression for smaller file sizes                                                                               |
| HDF5          | HDF5             | A versatile data model that can represent complex data objects and a wide variety of metadata                                                                                                                                              |
| ASCII         | CSV              | CSV (Comma-Separated Values) is a simple, human-readable format for tabular data ([more](<https://en.wikipedia.org/wiki/Comma-separated_values#:~:text=Comma%2Dseparated%20values%20(CSV),typically%20represents%20one%20data%20record.>)) |
| ASCII         | GeoCSV           | An extension of the CSV format with extensive metadata ([more](http://geows.ds.iris.edu/documents/GeoCSV.pdf))                                                                                                                             |
| ASCII         | SPECFEM          | A format used for specific geophysical modeling applications ([more](https://specfem.org/))                                                                                                                                                |
| GeoModelGrids | GeoModelGrids    | A specialized format for geophysical and geological models ([more](https://geomodelgrids.readthedocs.io/en/latest/))                                                                                                                       |

## Model Variable Naming and Unit Requirements

To ensure consistency and compatibility, the use of model variables conforming to the following list of variable names and units is required. Please adhere to these naming conventions and units when submitting or utilizing CVM tools.

| **Variable Name**     | **Units**                                                     |
| --------------------- | ------------------------------------------------------------- |
| **Vs**                | (km/s or m/s)                                                 |
| **Vp**                | (km/s or m/s)                                                 |
| **Vs (perturbation)** |                                                               |
| **Vp (perturbation)** |                                                               |
| **Density**           | (kg/m³ or g/cm³)                                              |
| **Rayleigh Phase**    | (km/s or m/s)                                                 |
| **Love Phase**        | (km/s or m/s)                                                 |
| **Rayleigh Group**    | (km/s or m/s)                                                 |
| **Love Group**        | (km/s or m/s)                                                 |
| **Depth**             | (km or m – positive downwards) (only for surfaces/interfaces) |

If a model variable cannot be selected from this list, an addition or clarification is required.

## Metadata

All CVM files include extensive metadata that follow the [CF Metadata Conventions](https://cfconventions.org/) and, as needed, introduce additional attributes like `source` data variable attribute and `data_layout` global attribute.

### Source

In addition to the standard CF variable attributes, each model data variable should contain a `source` attribute that describes the origin of the data for this variable:

- If the data is derived from observations, the `source` attribute should be set to **data-derived**.
- If the data is derived from an empirical formula, the `source` attribute should indicate how the variable was derived.

For example:

- `vp:source = data-derived`
- `vs:source = assumed to follow vp as vs = vp / sqrt(3) `

### Data Layout

Each model should also include a global attribute `data_layout`. This attribute specifies the layout of the data in the file and can take two possible values:

- `'vertex'` for vertex-based layout (values are specified at vertices)
- `'cell'` for cell-based layout (values are specified at the centers of grid cells)

Currently, the CVM-Tools support vertex-based values.

## Coordinate Systems

Earth models are often defined on a geographic grid that follows lines of constant latitude and longitude. However, for some models, a projected coordinate system, such as UTM, is preferred because it results in less local distortion. CVM primary formats use an extended netCDF format that includes both the projected coordinate system variables and the geographic latitude and longitude variables.

The primary coordinate system defines the coordinate system under which the model is described (geographic or UTM). This ensures consistency and clarity in the representation of spatial data. When setting up your netCDF file, specify the primary coordinate system to match the model's defined system.

Defining an auxiliary coordinate system is optional but offers several advantages:

- **Enhanced Versatility**: Provides additional spatial context, allowing data to be interpreted in multiple coordinate systems.
- **Improved Data Analysis**: Facilitates comparisons and transformations between different projections, aiding in more comprehensive analysis.
- **Consistency**: Ensures that various spatial datasets can be accurately integrated, maintaining consistency in geospatial representations.
- **User Flexibility**: Users can select the most appropriate coordinate system for their specific application, enhancing usability and flexibility.

These benefits collectively improve the robustness and usability of geospatial data stored in netCDF files.

For the primary coordinate systems, the variables should be:

| Geographic Coordinate System | Projected UTM Coordinates |
| ---------------------------- | ------------------------- |
| `longitude` and `latitude`   | `x` and `y`               |

If the primary coordinate variables are `longitude` and `latitude`, the auxiliary coordinates will be UTM's `easting` and `northing`. Conversely, if the primary coordinate system is UTM, the primary coordinate variables will be `x` and `y` (representing UTM easting and northing values, respectively), and the auxiliary coordinates will be the geographic `longitude`and `latitude` variables.
.

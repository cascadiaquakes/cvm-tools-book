# Tool Overview

## Introduction

This chapter provides an overview of the various tools available in the CVM-Tools package. Each tool is designed to facilitate specific tasks related to the storage, extraction, and visualization of CVMs. The primary tools focus on metadata and data storage, while the utility tools offer additional functionalities such as format conversion and data extraction.

## Primary Tools

### cvm_writer for 2D and 3D models

**Application**: Metadata and data storage  
**Description**: Reads a text 2D or 3D model metadata file and outputs the corresponding model metadata in GeoCSV and JSON formats. If a CSV model data file is also provided, the output can include the model in GeoCSV and/or netCDF formats.

**Usage**: Output metadata and/or model based on an input parameter file and a given CSV data file. The output can be one or more of the following:

- Metadata in GeoCSV
- Metadata in JSON
- Model in GeoCSV
- Model in netCDF

**Guide**: <a href="usage/cvm_writer.html">cvm_writer</a>

### cvm_writer_h5 (TESTING)

**Application**: Metadata and data storage  
**Description**: Reads text model metadata files and a CSV model data file, and outputs the model in HDF5 format.

**Usage**: Create a CVM model in HDF5 format based on input parameter files and given CSV data file(s).

**Guide**: <a href="usage/cvm_writer_h5.html">cvm_writer_h5</a>

### cvm_slicer

**Application**: Data extraction and plotting  
**Description**: Tool for interactively extracting data from a CVM netCDF file. Users can inspect the metadata, slice the data, plot, and save the sliced data. Slicing can be performed along the existing coordinate planes or as an interpolated cross-sectional slice through gridded data.

**Usage**: Extract data from a CVM netCDF file. Interactively, users can inspect the metadata, slice the data, plot, and save the sliced data.

**Guide**: <a href="usage/cvm_slicer.html">cvm_slicer</a>

## Support Tools

### convert_to_csv_2d

**Application**: Format conversion  
**Description**: Converts 2D netCDF or GeoJSON files to CSV format.

**Usage**: Converts 2D netCDF (.nc) or GeoJSON files into CSV format, extracting coordinate data (`x`, `y`) and associated metadata or attributes. Supports features like handling missing values and flattening multi-point geometries.

**Guide**: <a href="usage/convert_to_csv_2d.html">convert_to_csv_2d</a>

### hdf5_summary_info

**Application**: HDF5 information extraction  
**Description**: A utility tool designed to read and analyze HDF5 files. It provides a detailed summary of the file content, including global metadata, dimensions, and variables with their respective attributes and data ranges.

**Usage**: This script is for verifying the overall structure and integrity of HDF5 files, ensuring that they conform to expected formats and contain the necessary information for further processing or analysis.

**Guide**: <a href="usage/hdf5_summary_info.html">hdf5_summary_info</a>

### netcdf_summary_info

**Application**: netCDF information extraction  
**Description**: A utility tool designed to read and analyze netCDF4 classic files. It provides a detailed summary of the file content, including global metadata, dimensions, and variables with their respective attributes and data ranges.

**Usage**: This script is for verifying the overall structure and integrity of netCDF files, ensuring that they conform to expected formats and contain the necessary information for further processing or analysis.

**Guide**: <a href="usage/netcdf_summary_info.html">netcdf_summary_info</a>

### netcdf_to_cvm

**Application**: Format conversion  
**Description**: Converts a CF-compliant netCDF file to CVM netCDF standard.

**Usage**: Convert a netCDF file to the CVM netCDF standard.

**Guide**: <a href="usage/netcdf_to_cvm.html">netcdf_to_cvm</a>

### netcdf_to_geocsv

**Application**: Format conversion  
**Description**: Converts a CVM netCDF file to GeoCSV and/or outputs its metadata in JSON format.

**Usage**: Convert a CVM netCDF file to GeoCSV format and/or output its metadata in JSON format.

**Guide**: <a href="usage/netcdf_to_geocsv.html">netcdf_to_geocsv</a>

### netcdf-2d_to_geojson

**Application**: Format conversion  
**Description**: Converts a CVM netCDF or a GMT .grd file to GeoJSON.

**Usage**: To converts 2D netCDF (.nc) or .grd files into GeoJSON format, supporting rectangular and triangular grid representations. It can handle depth or elevation variables and allows decimation of data to improve performance.

**Guide**: <a href="usage/netcdf-2d_to_geojson.html">netcdf-2d_to_geojson</a>

### netcdf_to_h5

**Application**: Format conversion  
**Description**: Converts a CVM-compliant netCDF file to CVM HDF5.

**Usage**: Convert a netCDF file to the HDF5 format.

**Guide**: <a href="usage/netcdf_to_hd.html">netcdf_to_hd\*</a>

### show_file_structure

**Application**: Format conversion  
**Description**: Converts a CVM-compliant netCDF file to CVM HDF5.

**Usage**: reads a file (either HDF5 or netCDF format) and prints its structure, including the file name, size, and type. It is useful for quickly inspecting the contents of the model data files.

**Guide**: <a href="usage/show_file_structure.html">netcdf_to_hd\*</a>

### verify_installation

**Application**: Installation validation  
**Description**: Ensure that all required packages are installed and that a specific netCDF file can be read successfully. This guide will walk you through how to use the script to verify your installation.
.

**Usage**: Verify the installation.

**Guide**: <a href="usage/verify_installation.html">verify_installation</a>

### netcdf_to_geomodelgrids (under development)

**Application**: Format conversion  
**Description**: Converts a CVM netCDF file to GeoModelGrids format.

**Usage**: Convert a CVM netCDF file to the GeoModelGrids format.

**Guide**: <a href="#">netcdf_to_geomodelgrids</a>

### netcdf_to_specfem (under development)

**Application**: Format conversion  
**Description**: Converts a CVM netCDF file to SPECFEM format.

**Usage**: Convert a CVM netCDF file to the SPECFEM format.

**Guide**: <a href="#">netcdf_to_specfem</a>

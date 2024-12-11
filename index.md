# Welcome to the CVM-Tools Tutorials

## Project Overview

The [CVM-Tools repository](https://cvmweb-albfa-xk4p5bggbtl6-1199205512.us-east-2.elb.amazonaws.com/) hosts Python 3 tools developed to support the Cascadia Community Velocity Model ([CVM](https://cascadiaquakes.org/cvm/)) working group's effort in constructing a three-dimensional representation of subsurface material properties for the Cascadia region. These tools facilitate the storage, extraction, and visualization of the CVM through uniform and self-contained data formats.

## About This Tutorial

This tutorial features a collection of individual guides on the utilization of CVM-Tools. Where needed, guides include examples and step-by-step instructions to help you use CVM-Tools. The guides are broken into three sections: **Introduction**, **Primary Tools**, and **Utility Tools**.

The **Introduction** section provides an overview of standards and rules that apply to all CVM-Tools and includes:

- **Standards and Conventions:** This section gives insight into the essential standards and conventions that CVM-Tools are based on. It covers the supported file formats, metadata requirements, and coordinate systems, ensuring that all users follow a uniform approach to creating, distributing, and utilizing CVM velocity models.
- **Code Repository Overview:** Provides an overview of the CVM Git repository.
- **Setup Guide:** Learn how to install the necessary dependencies and configure your environment for using CVM-Tools.
- **Tool Overview:** Offers an overview of the various tools available in the CVM-Tools package.

The **Primary Tools** section provides tutorials on the primary CVM tools that are used to create, maintain, extract, and visualize CVM data. This section include:

- **Introduction:** Get introduced to the CVM data files that will be used in this guide.
- **Parameter Files:** Explore how to structure parameter files for constructing metadata.
- **cvm_writer:** Learn how to use the `cvm_writer` tool to convert raw CSV model data to CVM model files in netCDF.
- **cvm_writer_h5:** Learn how to use the `cvm_writer_h5` tool to convert raw CSV model data to CVM model files in HDF5.
- **cvm_slicer:** Learn how to use `cvm_slicer` to visualize and save netCDF CVM data.

The **Utility Tools** section provides tutorials on various CVM utility tools to help with data conversion and inspection of CVM files. These tools include:

- **convert_to_csv_2d:** A utility tool for converting 2D NetCDF or GeoJSON files to CSV format, extracting coordinate data (`x`, `y`) and associated metadata or attributes.
- **netcdf_to_geocsv:** A utility tool for converting a netCDF CVM file to the corresponding CSV, GeoCSV format and optionally output its JSON metadata.
- **netcdf_to_h5:** A utility tool for converting an existing CVM-compliant netCDF file to HDF5 format.
- **netcdf_to_cvm:** A utility tool for converting an existing netCDF CVM file to the corresponding CVM-compliant netCDF file. This tool will add any missing CVM attributes based on the provided metadata files.
- **netcdf_summary_info:** A utility tool designed to read, analyze, and provide a comprehensive summary of a netCDF4 classic file’s contents. This script outputs detailed information about dimensions, variables, attributes, and data ranges within the netCDF file, helping users to verify the overall structure and integrity of the file.
- **hdf5_summary_info:** A utility designed to read, analyze, and provide a comprehensive summary of an HDF5 file’s contents. This script outputs detailed information about groups, datasets, attributes, and data ranges within the HDF5 file, helping users to verify the overall structure and integrity of the file.

To get started, if you are already familiar with CVM standards and conventions, feel free to jump into the {doc}`setup_guide` section, which will walk you through the installation process and initial configuration. Otherwise, before diving into the tools, it's essential to understand the standards and conventions we follow by learning about the {doc}`standards_and_conventions`.

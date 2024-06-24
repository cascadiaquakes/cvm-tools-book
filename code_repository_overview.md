# Code Repository Overview

The CVM-Tools are hosted on GitHub at [https://github.com/cascadiaquakes/cvm-tools](https://github.com/cascadiaquakes/cvm-tools). This repository contains all the necessary files for using and developing the tools. Below is an overview of the repository structure:

## Repository Contents

- **README.md**: Provides an overview of the repository and instructions for getting started.
- **documents/**: Contains presentations and guides related to CVM-Tools.
  - `2024-01-08-CRESCENT-CVM.pptx`
  - `2024-05-14-Tutorial-on-CVM-Tools.pptx`
  - `2024-05-14-Tutorial-on-CVM-Tools_Guide.pdf`
- **lib/**: Python library of functions used by the tools.
  - `netcdf_to_geocsv_lib.py`
  - `shared_lib.py`
  - `slicer_lib.py`
  - `writer_lib.py`
- **prop/**: Property files for configuring the tools.
  - `netcdf_to_geocsv_prop.py`
  - `shared_prop.py`
  - `slicer_prop.py`
  - `writer_prop.py`
- **requirements.txt**: Lists the Python dependencies needed to run the tools.
- **sample-files/**: Sample data files for demonstration and testing.
  - `Cascadia-ANT+RF-Delph2018/`
    - `Cascadia-ANT+RF-Delph2018.r0.1.csv`
    - `Cascadia-ANT+RF-Delph2018.r0.1.nc`
    - `Cascadia-ANT+RF_data.txt`
    - `Cascadia-ANT+RF_meta.txt`
    - `Cascadia_ANT+RF_Delph2018.txt.gz`
    - `simple_plotter_prop.py`
  - `casc1.6_velmdl/`
    - `README`
    - `casc16-velmdl_meta.txt`
    - `simple_plotter_prop.py`
- **src/**: Source code for the tools.
  - `cvm_slicer.py`
  - `cvm_writer.py`
  - `cvm_writer_h5.py`
  - `hdf5_summary_info.py`
  - `netcdf_summary_info.py`
  - `netcdf_to_cvm.py`
  - `netcdf_to_geocsv.py`
  - `verify_installation.py`
- **template/**: Templates for metadata and configuration files.
  - `global_metadata_template.txt`
  - `variables_metadata_template.txt`

This structure ensures that all necessary components are organized and easily accessible.

Next, we will learn how to install the necessary dependencies and configure your environment for using CVM-Tools.

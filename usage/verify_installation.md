# verify_installation

## Overview

The `verify_installation.py` script is designed to ensure that all required packages are installed and that a specific netCDF file can be read successfully. This guide will walk you through how to use the script to verify your installation.

## Prerequisites

1. **Python Environment**: Ensure you have Python installed on your system.
2. **requirements.txt**: A file listing all the necessary packages for your project.
3. **netCDF File**: Ensure you have the netCDF file located at `../sample-files/Cascadia-ANT+RF-Delph2018/Cascadia-ANT+RF-Delph2018.r0.1.nc` relative to the script's directory.

## Setup

1. **Setup**: Follow the the steps in the **setup guide**.
2. **Navigate to the `src` Directory**: Open a terminal or command prompt and navigate to the directory containing the `verify_installation.py` script.

## Usage

1. **Run the Script**: Execute the script using Python:

   ```bash
   python verify_installation.py
   ```

2. **Script Execution**: The script performs the following steps:

   - **Read `requirements.txt`**: Reads the required packages from `requirements.txt` located in the parent directory.
   - **Check and Install Packages**: Verifies if the required packages are installed. If not, attempts to install them using `pip`.
   - **Basic Functionality Tests**: Performs basic tests using `numpy`, `pandas`, and `matplotlib` to ensure they are functioning correctly.
   - **netCDF File Check**: Reads the netCDF file and prints a summary of its dimensions and variables.

3. **Output**: The script will output the status of each step, indicating whether the packages are installed correctly, whether the basic functionality tests passed, and whether the netCDF file was read successfully.

## Example Output

Upon successful execution, you should see output similar to the following:

```
Reading requirements.txt...
Checking required packages...
numpy is installed correctly.
pandas is installed correctly.
matplotlib is installed correctly.
Running basic functionality tests...
All basic functionality tests passed.
Checking netCDF file...
netCDF file: ../sample-files/Cascadia-ANT+RF-Delph2018/Cascadia-ANT+RF-Delph2018.r0.1.nc
Dimensions: dict_keys([...])
Variables: dict_keys([...])
Installation confirmed. All tests passed successfully.
```

If there are any issues, the script will output an appropriate error message indicating the problem.

## Troubleshooting

- **Missing `requirements.txt`**: Ensure the `requirements.txt` file is located in the parent directory of the script.
- **netCDF File Not Found**: Ensure the netCDF file is located at the specified path relative to the script.
- **Package Installation Issues**: Ensure you have internet access and the necessary permissions to install packages using `pip`.

By following this guide, you should be able to verify that your environment is correctly set up and that all required packages and files are in place.

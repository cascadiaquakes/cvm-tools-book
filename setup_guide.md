# Setup Guide

## Prerequisites

This package has been tested under Python 3.12.0 on macOS 14.4.1. It may work with older Python 3 versions, but Python 3.9 is the minimum recommended version. We encourage utilizing the tools with a more recent version of Python for the best performance and compatibility.

## Installation Steps

1. **Clone the Repository:**

   ```
   git clone https://github.com/your-username/cvm-tools.git
   cd cvm-tools
   ```

2. **Set Up a Virtual Environment:**

   ```
   python3 -m venv env
   source env/bin/activate 
   ```

3. **Install the Dependencies:**

   ```
   pip install -r requirements.txt
   ```

4. **Verify Installation:**

   Run the simple `verify_installation.py` script to ensure everything is set up correctly. This is a minimum test to make sure packages are installed and to verify that a sample netCDF file (`sample-files/Cascadia-ANT+RF-Delph2018/Cascadia-ANT+RF-Delph2018.r0.1.nc`) can be read.

   ```
   python src/verify_installation.py
   ```

Once your environment is set up, you can proceed to explore the various notebooks and functionalities provided by CVM-Tools.

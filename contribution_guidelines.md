# Model Contribution Guidelines

To contribute your Cascadia Earth model to CRESCENT:

- **Study Area Requirement**: The model must cover the CRESCENT study area (latitude: 39° to 52°, longitude: -130° to -116°).
- **Standards Compliance**: All models must adhere to the <a href="./standards_and_conventions.html" target="_blank">CVM Standards and Conventions</a>.
- **Model Preparation**: Follow the steps outlined in the **How to Prepare Your Model** section below.
- **Submission Request**: Visit the <a href="https://github.com/cascadiaquakes/CRESCENT-CVM/issues" target="_blank">CRESCENT-CVM GitHub Issue Page</a> and create a submission request.
  - Your request **must include a download link** to your model.
  - **Do not attach model files** directly to the issue request.

### How to Prepare Your Model

To ensure your model complies with CVM standards, please follow the following conversion and validation steps depending on your original model's data format.

#### Format Conversion

##### CSV to netCDF4 or HDF5

- If your original model is in CSV format and you want to convert it to netCDF4, please follow the steps outlined under <a href="./usage/cvm_writer.html" target="_blank">cvm_writer</a>.
- If you want to convert your CSV files to HDF5 format, please follow the steps outlined under <a href="./usage/cvm_writer_h5.html" target="_blank">cvm_writer_h5</a>.

##### netCDF to CVM-compatible netCDF4

If your original model is in a valid netCDF3 or netCDF4 Classic format, please follow the steps under <a href="./usage/netcdf_to_cvm.html" target="_blank">netcdf_to_cvm</a> to ensure that it complies with the CVM standards.

#### Model File Validation

##### Validating netCDF Files and Creating the metadata JSON file

- Please verify the netCDF file's metadata content using <a href="./usage/cvm_inspector.html" target="_blank">cvm_inspector</a>.

- Please verify the netCDF file's metadata and create a slice to validate the file content using <a href="./usage/cvm_slicer.html" target="_blank">cvm_slicer</a>.

- Use the <a href="./usage/netcdf_to_geocsv.html" target="_blank">netcdf_to_geocsv</a> tool with `-m true` option to create a JSON file containing your files metadata.

##### Validating HDF5 Files

- Please verify their metadata and create a slice to validate the file content using the **cvm_slicer_h5 Tool (coming soon)**.

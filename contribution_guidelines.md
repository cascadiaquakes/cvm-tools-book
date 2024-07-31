# Model Contribution Guidelines

To contribute your Cascadia Earth model to CRESCENT:

- The model must be for the CRESCENT study area (latitude: 39° to 52°, longitude: -130° to -116°)
- The file format should be either CVM-compatible netCDF4 Classic or CVM-compatible HDF5 format.
- <a href ="https://cvmweb-albfa-xk4p5bggbtl6-1199205512.us-east-2.elb.amazonaws.com/request" target="_blank">Contact us to request a model submission</a>

### Preparing Your Model

To ensure your model complies with CVM standards, please follow the following conversion and validation steps depending on your original model's data format.

#### Format Conversion

##### CSV to netCDF4 or HDF5

- If your original model is in CSV format and you want to convert it to netCDF4, please follow the steps outlined under <a href="usage/cvm_writer.html" target="_blank">cvm_writer</a>.
- If you want to convert your CSV files to HDF5 format, please follow the steps outlined under <a href="usage/cvm_writer_h5.html" target="_blank">cvm_writer_h5</a>.

##### netCDF to CVM-compatible netCDF4

If your original model is in a valid netCDF3 or netCDF4 Classic format, please follow the steps under <a href="usage/netcdf_to_cvm.html" target="_blank">netcdf_to_cvm</a> to ensure that it complies with the CVM standards.

#### Model File Validation

##### Validating netCDF Files

- For models in netCDF format, please verify their metadata and create a slice to validate the file content using <a href="usage/cvm_slicer.html" target="_blank">cvm_slicer</a>.

##### Validating HDF5 Files

- For models in HDF5 format, please verify their metadata and create a slice to validate the file content using the **cvm_slicer_h5 Tool (coming soon)**.

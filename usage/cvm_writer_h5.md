# cvm_writer_h5 (TESTING)

This tool is in testing stage.
In this tutorial, we will use the `cvm_writer_h5` tool to convert the `Cascadia_ANT+RF_Delph2018` raw data into a CVM model file in HDF5 format. To create CVMs in HDF5 format, we need:

- The model data files in CSV format
- A global parameter file
- Parameter file(s) for the variables

The parameter files are based on the templates from the `template` directory.

For converting the `Cascadia_ANT+RF_Delph2018` model to HDF5, we need one data file and one parameter file since only one dataset exists in the model.

As you note below, the steps needed to convert the model are similar to those of the **cvm_writer** to create a netCDF file.

## Step 1: Navigate to the Model Directory

Change your directory to the model directory:

```sh
cd sample-files/Cascadia-ANT+RF-Delph2018
```

## Step 2: Prepare the Data File

You can skip this step if you did it under the **cvm_writer** tutorial.

The `Cascadia_ANT+RF_Delph2018.txt.gz` file is the raw data file for the model. Unzip it and copy it to a file for testing (e.g., `Cascadia-ANT+RF_data.txt`). This will be our model's data file. All model data files need to have a header as their first line that identifies the columns in the file using the same delimiter between column names as used for the data. Place the following header as the first line in `Cascadia-ANT+RF_data.txt`:

```sh
longitude latitude depth vs
```

<div class="figure-container" style="display: flex; justify-content: space-around; align-items: center;">
    <figure>
        <img src="../_images/step2_data_file.png" alt="Data File" width="300"/>
        <figcaption>Data file with the required header added. The delimiter between column names should be the same as used for the data.</figcaption>
    </figure>
</div>

## Step 3: Prepare the Metadata File

Now, we need model metadata files. The metadata files contain the model metadata as text. Templates for the metadata files are available under the `template` folder. Two metadata files are needed: one global based on `template/global_metadata_template.txt` and another for variables based on `template/variables_metadata_template.txt`. When creating HDF5 files, we need one **data file** and one **variables_metadata file** per dataset. In this case, `Cascadia_ANT+RF_Delph2018` has only one dataset.

For this tutorial, you do not need to copy templates. We already have the necessary metadata file for the global attributes as `Cascadia-ANT+RF_global_meta.txt` and for variables as `Cascadia-ANT+RF_meta.txt` placed under this directory.

<figure>
    <img src="../_images/step3_metadata_file.png" alt="Metadata File" width="500"/>
    <figcaption>A view of the global metadata file.</figcaption>
</figure>

These parameter files are the same as those used by the **cvm_writer** tool, but pay particular attention to the following HDF5-specific attributes in the parameter files where we define the HDF5 groupings:

`Cascadia-ANT+RF_global_meta.txt` has the following definitions to define **groups** in our HDF5:

```bash
> groups
     volumes = volumes
     surfaces = surfaces
```

The **volumes** group will be used to store 3D data and the **surfaces** group will be used to store the 2D data. In our case, our data is 3D and the **volumes** group will be used.

`Cascadia-ANT+RF_meta.txt` has the following definitions to define **dataset group** in our HDF5:

```bash
- dataset_group = velocity
```

The **velocity** dataset group will be used to store 3D data under the **volumes** group defined in the global parameter file above.

For detailed instructions on how to create these parameter files, see the **Parameter File Structure** guide.

## Step 4: Create the Model File

Now, create the model file by running:

```sh
python ../../src/cvm_writer_h5.py -m Cascadia-ANT+RF_meta.txt -g Cascadia-ANT+RF_global_meta.txt -o Cascadia-ANT+RF-test -d Cascadia-ANT+RF_data.txt
```

- `-m Cascadia-ANT+RF_meta.txt` tells `cvm_writer` that the variables metadata file is `Cascadia-ANT+RF_meta.txt`.
- `-g Cascadia-ANT+RF_global_meta.txt` tells `cvm_writer` that the global metadata file is `Cascadia-ANT+RF_global_meta.txt`.
- `-o Cascadia-ANT+RF-test` is the name of the output file (**no file extension should be included**).
- `-d Cascadia-ANT+RF_data.txt` tells the code where it can find the model data.

After running this command, you should see a new file `Cascadia-ANT+RF-test.h5`, which is our model in HDF5.

## Step 5: Examine the HDF5 File Content

To examine the HDF5 file content, use the `hdf5_summary_info.py` script to summarize the created HDF5 file. Upon execution, the script will prompt you for the name of the HDF5 file to summarize. It will then read the HDF5 file and provide a summary of the metadata and data contained in the file. Successful execution of this step indicates that the general structure of the HDF5 file is correct and allows you to examine the data and metadata contained in the file to verify.

Run the following command:

```sh
python ../../src/hdf5_summary_info.py
```

<figure>
    <img src="../_images/hdf5_summary_prompt.png" alt="Summary Prompt" width="400"/>
    <figcaption>Prompt for HDF5 file name.</figcaption>
</figure>

After providing the file name, you will see a summary of the HDF5 file content.

<figure>
    <img src="../_images/hdf5_summary_output.png" alt="Summary Output" width="400"/>
    <figcaption>Summary of the HDF5 file content.</figcaption>
</figure>

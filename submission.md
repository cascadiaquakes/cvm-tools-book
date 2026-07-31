# Model Contribution Instructions

## Requirements

To contribute your velocity model to the CRESCENT Community Velocity Model Viewer please first make sure your model meets the following requirements:

- **Study Area Requirement**: The majority of the model must fall within the CRESCENT geographic footprint (latitude: 39° to 52°, longitude: -130° to -116°) or be completely contained within it. If your model covers a larger region, you are welcome to submit a subset that falls within this range.
- **Peer-reviewed**: All models must be described in a peer-reviewed publication with an associated DOI. Please include a publicly accessible link to the peer-reviewed article that describes the model.
- **Standards Compliance**: All models must adhere to the <a href="./standards_and_conventions.md" target="_blank">CVM Standards and Conventions</a>.

If your model meets the requirements above, please follow the steps in the sections below.

(model-metadata)=
## Model Metadata

Each model included in the CRESCENT CVM Repository is described by a standard set of metadata fields that make it discoverable and comparable in the viewer.

### Required Fields

- **MODEL TYPE:** Model quantities provided (e.g., V<sub>s</sub>, V<sub>p</sub>, V<sub>p</sub>/V<sub>s</sub>, density, V<sub>s</sub> perturbation, phase or group velocity).
- **METHODOLOGY:** Imaging method used to derive the model (e.g., ambient noise tomography, receiver functions, full-waveform inversion, joint inversion).
- **MINIMUM LONGITUDE / MAXIMUM LONGITUDE / LONGITUDE RESOLUTION:** Spatial extent in longitude and grid spacing.
- **MINIMUM LATITUDE / MAXIMUM LATITUDE / LATITUDE RESOLUTION:** Spatial extent in latitude and grid spacing.
- **MINIMUM DEPTH / MAXIMUM DEPTH:** Depth range covered by the model (positive downward, km).
- **CONSTRAINED PARAMETERS:** Which model variables are directly constrained by the observations used in the study, versus which are derived or unconstrained assumptions. This is important context for users choosing between models in the viewer (see the disclaimer below).

### Optional Fields

- **VELOCITY MODEL BACKGROUND:** Reference or 1D background model used as a starting point for the inversion.
- **DENSITY BACKGROUND:** How density was assigned if it was not directly inverted (e.g., Nafe-Drake, empirical scaling).
- **UNCERTAINTY:** Formal or bootstrap uncertainty estimates if provided.
- **NOTES:** Any additional context relevant to model users.

:::{admonition} Variable naming and case
:class: tip
The viewer displays and filters models by variable name. To keep the filter list consistent across models, please use the canonical variable names below and match their capitalization exactly. Do not submit lowercase variants (e.g., use `Vs`, not `vs`).

- `Vs`, `Vp`, `Density`
- `Vs_perturbation`, `Vp_perturbation`
- `Rayleigh_Phase`, `Rayleigh_Group`, `Love_Phase`, `Love_Group`

Units should follow the CVM standards: V<sub>s</sub> and V<sub>p</sub> in km/s, density in g/cm³.
:::

:::{admonition} Constrained vs unconstrained parameters
:class: important
Not every variable that a model file contains is directly constrained by the analysis in the corresponding publication. For example, an ambient noise or receiver function study may constrain V<sub>s</sub> directly while carrying V<sub>p</sub> and density as fixed background values or empirical scalings.

Please state clearly in the **CONSTRAINED PARAMETERS** field which variables are constrained by the study. Users of the viewer are advised to consult the model description page before using unconstrained variables in their own analyses. Where practical, submit only the constrained variables; if you include unconstrained variables for completeness, please flag them explicitly.
:::

## Step 1: Prepare your model

Your model can be submitted in any of the CVM-compliant formats below. If your original file is not already CVM-compliant, use the CVM-Tools utilities in this book to convert and validate it.

### Format Conversion

**Please note**: CVM follows a specific variable naming convention (see the <a href="./standards_and_conventions.md#model-variable-naming-and-unit-requirements">Model Variable Naming and Unit Requirements</a> section of <a href="./standards_and_conventions.md">Standards and Conventions</a>). Please rename your variables accordingly before conversion.

#### CSV to netCDF4 or HDF5

- If your original model is in CSV format and you want to convert it to netCDF4, please follow the steps outlined under <a href="./usage/cvm_writer_3d.md" target="_blank">cvm_writer_3D</a> for 3D models or <a href="./usage/cvm_writer_2d.md" target="_blank">cvm_writer_2D</a> for 2D models.
- If you want to convert your CSV files to HDF5, please follow the steps outlined under <a href="./usage/cvm_writer_h5.md" target="_blank">cvm_writer_h5</a>.

#### netCDF to CVM-compliant netCDF4

If your original model is in a valid netCDF3 or netCDF4 Classic format, please follow the steps under <a href="./usage/netcdf_to_cvm.md" target="_blank">netcdf_to_cvm</a> to bring it into compliance with the CVM standards.

### Model File Validation

#### Validating netCDF Files and Creating the Metadata JSON File

- Verify the netCDF file's metadata using <a href="./usage/cvm_inspector.md" target="_blank">cvm_inspector</a>.
- Verify the metadata and slice the file to validate its content using <a href="./usage/cvm_slicer.md" target="_blank">cvm_slicer</a>.
- Use the <a href="./usage/netcdf_to_geocsv.md" target="_blank">netcdf_to_geocsv</a> tool with the `-m true` option to create a JSON file containing your model's metadata. The viewer reads this sidecar JSON to populate the model description panel.

#### Validating HDF5 Files

- Verify the metadata and slice the file to validate its content using the **cvm_slicer_h5 Tool (coming soon)**.

## Step 2: Prepare a Markdown file describing your model

Each velocity model included in the CRESCENT CVM Repository has a corresponding page describing the model in this JupyterBook. For example, the page describing the model of Delph et al. (2018) can be found <a href="https://cascadiaquakes.github.io/cvm-tools-book/delph-epsl-2018/" target="_blank">here</a>.

### Descriptive Metadata

To create a JupyterBook page for your model you will need to define the metadata fields listed in the {ref}`model-metadata` section above.

### Model Page Template

To create a JupyterBook page describing your model please use the following template.

::::{admonition} Model Markdown Template
:class: dropdown

````markdown
# {AuthorLastName} et al. ({Year})

## {Model / Paper Title}

{Author list}

[![DOI](https://img.shields.io/badge/DOI-{DOI_URL_ENCODED}-blue)](https://doi.org/{DOI})

In the DOI badge URL, replace `/` with `%2F` (URL encoding).

:::{figure} ./{figure_filename}.jpg
:label: fig:{short_label}

{Figure caption describing the model, region, and key observations.}
:::

## Abstract

{Abstract text describing the model and its scientific context. Can be taken directly from the corresponding publication.}

## Model Information

- **MODEL TYPE:** {V_s, V_p, V_p/V_s, density, V_s perturbation, phase/group velocity, etc.}
- **METHODOLOGY:** {imaging method, e.g. ambient noise tomography, receiver functions, joint inversion}
- **MINIMUM LONGITUDE:** {value}
- **MAXIMUM LONGITUDE:** {value}
- **LONGITUDE RESOLUTION:** {value}
- **MINIMUM LATITUDE:** {value}
- **MAXIMUM LATITUDE:** {value}
- **LATITUDE RESOLUTION:** {value}
- **MINIMUM DEPTH:** {value} km
- **MAXIMUM DEPTH:** {value} km
- **CONSTRAINED PARAMETERS:** {which variables are directly constrained by the study, and which are background/derived}
- **VELOCITY MODEL BACKGROUND:** {optional}
- **DENSITY BACKGROUND:** {optional}
- **UNCERTAINTY:** {optional}
- **NOTES:** {optional}
````

::::

## Step 3: Submit your model to the repository

- **Submission Request**: Visit the <a href="https://github.com/cascadiaquakes/CRESCENT-CVM/issues" target="_blank">CRESCENT-CVM GitHub Issue Page</a> and create a submission request.
  - Your request must include a **publicly accessible download link** to your model file (netCDF or HDF5). **Do not attach model files directly** to the issue.
  - Your request must include a download link to your Markdown file containing the model description.
  - Your request must include your contact information so we can get in touch if we have questions and notify you once your model is included in the viewer.

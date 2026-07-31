# CRESCENT Community Velocity Model Repository and Viewer

The <a href="https://cascadiaquakes.org">Cascadia Region Earthquake Science Center (CRESCENT)</a>  <a href="https://cascadiaquakes.github.io/cvm-tools-book/">**Community Velocity Model Repository**</a> and <a href="https://cvm.cascadiaquakes.org">**CVM Viewer**</a> is a community resource for the collection, documentation, and dissemination of peer-reviewed 3D and 2D seismic velocity models of the crust and mantle within the Cascadia Subduction Zone and surrounding regions. The repository is designed to support reproducible earthquake science by providing standardized access to curated velocity models derived from a wide range of seismic imaging methods.

This effort is part of the broader mission of CRESCENT to advance understanding of earthquake science in the Pacific Northwest through open science, community model development, and shared cyberinfrastructure.

## Motivation

Three-dimensional velocity models are foundational datasets for studies of subduction zone processes, earthquake source imaging, ground motion simulation, and seismic hazard. Over the past decade, advances in seismic tomography, including full-waveform inversion, joint ambient noise and receiver function inversion, and increasingly dense seismic instrumentation such as nodal arrays and distributed acoustic sensing, have enabled the development of high-resolution regional velocity models that complement broader continental-scale models.

However, these models are often:
- Distributed across individual publications and/or repositories,
- Produced using heterogeneous formats, conventions, and metadata,
- Difficult to discover, compare, or reuse.

The CRESCENT Community Velocity Model Repository addresses these challenges by providing:
- A centralized, openly accessible collection of peer-reviewed velocity models,
- Consistent documentation describing how each model was generated and which parameters are constrained,
- A visualization tool that permits model comparison in 2D and 3D, interactive slicing, extraction, and download in standardized formats.

## Scope

We welcome 3D and 2D velocity models describing the seismic properties (V<sub>p</sub>, V<sub>s</sub>, density, and derived quantities such as V<sub>p</sub>/V<sub>s</sub>, perturbations, and surface wave phase or group velocities) of the crust and mantle in the Cascadia region. Models generated with a variety of imaging techniques, including ambient noise tomography, teleseismic body waves, surface wave dispersion, receiver functions, joint inversions, and machine-learning based approaches, are all in scope.

The only requirements are that any velocity model submitted for inclusion into the repository:
- Is primarily located within the **CRESCENT geographic footprint** (Cascadia), and
- Has been described in **peer-reviewed publications** with an associated DOI.

## Repository Structure

Each model included in the repository consists of:
1. A downloadable model file in the standardized CVM netCDF (or HDF5) format, and
2. A corresponding **Markdown description page** (rendered into this JupyterBook) covering the publication DOI, methodology, spatial extent, and which parameters are constrained.

Description pages follow a standardized Markdown template to ensure clarity and consistency while allowing contributors to highlight the unique aspects of their work.

## Visualization

Models hosted in this repository are integrated into the <a href="https://cvm.cascadiaquakes.org" style="color:#6fa8dc; font-weight:bold;">**CRESCENT CVM Viewer**</a>, enabling interactive exploration of crustal and mantle structure in map view, depth slices, and cross sections. The viewer supports side-by-side model comparison, extraction, and download in standardized formats. It is intended as a discovery and comparison tool and does not replace citation of the original peer-reviewed publications.

## Metadata

For a description of the model fields and other metadata please review the {ref}`model-metadata` section.

## Project Contacts

The CRESCENT Community Velocity Model Repository is developed and maintained by the CRESCENT cyberinfrastructure team in collaboration with the broader Cascadia earthquake science community. Individual models remain the intellectual property of their original authors.

**Amanda M. Thomas**  
amthom@ucdavis.edu  
Department of Earth and Planetary Sciences, University of California, Davis  

**William Marfo**  
wmarfo@ucdavis.edu  
Cascadia Region Earthquake Science Center    
Department of Earth and Planetary Sciences, University of California, Davis

**Loïc Bachelot**  
lbachelo@uoregon.edu  
Cascadia Region Earthquake Science Center  
Department of Earth Sciences, University of Oregon


## Acknowledgments

This project is supported by the **National Science Foundation** through the Cascadia Region Earthquake Science Center (CRESCENT).

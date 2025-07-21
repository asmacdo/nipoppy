# Nipoppy

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.8084759.svg)](https://doi.org/10.5281/zenodo.8084759)
[![PyPI - Version](https://img.shields.io/pypi/v/nipoppy)](https://pypi.org/project/nipoppy/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/license/mit)
[![codecov](https://codecov.io/gh/nipoppy/nipoppy/graph/badge.svg?token=SN38ITRO4M)](https://codecov.io/gh/nipoppy/nipoppy)
[![https://github.com/psf/black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://black.readthedocs.io/en/stable/)
[![Documentation Status](https://readthedocs.org/projects/nipoppy/badge/?version=latest)](https://nipoppy.readthedocs.io/en/latest/?badge=latest)

<img alt="Nipoppy logo" src="https://raw.githubusercontent.com/nipoppy/nipoppy/refs/heads/main/logo/logo_square.svg" width=100px style="float:right">

Nipoppy is a lightweight framework for standardized organization and processing of neuroimaging-clinical datasets. Its goal is to help users adopt the
[FAIR](https://www.go-fair.org/fair-principles/) principles
and improve the reproducibility of studies.

The framework includes three components:

1. A protocol for data organization, curation and processing, with steps that include the following:
    - **Organization** of raw data, including conversion of raw DICOMs (or NIfTIs) to [BIDS](https://bids.neuroimaging.io/)
    - **Processing** of imaging data with existing or custom pipelines
    - **Tracking** of data availability and processing status
    - **Extraction** of imaging-derived phenotypes (IDPs) for downstream statistical modelling and analysis

    ![Nipoppy protocol](https://raw.githubusercontent.com/nipoppy/nipoppy/main/docs/source/_static/img/nipoppy_protocol.jpg)

2. A specification for dataset organization that extends the [Brain Imaging Data Structure (BIDS) standard](https://bids.neuroimaging.io/) by providing additional guidelines for tabular (e.g., phenotypic) data and imaging derivatives.

```mermaid
graph TB
    A["&lt;dataset_root&gt;"]

    A --> B["📄 global_config.json"]
    A --> C["📄 manifest.tsv"]
    A --> D["📁 pipelines"]
    A --> E["📁 containers"]
    A --> F["📁 sourcedata"]
    A --> G["📁 tabular"]
    A --> H["📁 bids"]
    A --> I["📁 derivatives"]
    A --> J["📁 code"]
    A --> K["📁 logs"]
    A --> L["📁 scratch"]

    F --> M["📁 tabular"]
    F --> N["📁 imaging"]
    N --> O["📁 pre-reorg"]
    N --> P["📁 post-reorg"]
    N --> Q["📄 curation_status.tsv"]

    G --> R["📄 demographics.tsv"]
    G --> S["📁 assessments"]

    I --> T["📁 fmriprep"]
    I --> U["📄 processing_status.tsv"]
    T --> V["📁 20.2.7"]
    T --> Y["📁 23.1.3"]
    T --> Z["📁 ..."]
    V --> W["📁 output"]
    V --> X["📁 idp"]

    %% Styling with colors matching original
    classDef directory fill:#f9d71c,stroke:#333,stroke-width:2px,color:#000
    classDef createdFile fill:#fff3e0,stroke:#333,stroke-width:2px,color:#000
    classDef userConfig fill:#e8f5e8,stroke:#333,stroke-width:2px,color:#000
    classDef userTabular fill:#e1f5fe,stroke:#333,stroke-width:2px,color:#000
    classDef tracking fill:#f3e5f5,stroke:#333,stroke-width:2px,color:#000
    classDef derivatives fill:#ffebee,stroke:#333,stroke-width:2px,color:#000

    class A,D,E,F,G,H,I,J,K,L,M,N,O,P,S,T,V,W,X,Y,Z directory
    class C createdFile
    class B userConfig
    class R userTabular
    class Q,U tracking

    %% Legend
    subgraph Legend["Legend"]
        L1["📁 Directory"]:::directory
        L2["📄 File"]:::createdFile
        L3["Created by nipoppy init"]:::createdFile
        L4["User-provided configuration files"]:::userConfig
        L5["User-provided tabular study data"]:::userTabular
        L6["Tracking files"]:::tracking
        L7["Imaging derivatives data"]:::derivatives
    end
```

3. A **command-line interface** and **Python package** that provide user-friendly tools for applying the framework. The tools build upon existing technologies such as the [Apptainer container platform](https://apptainer.org/) and the [Boutiques descriptor framework](https://boutiques.github.io/). Several existing containerized pipelines are supported out-of-the-box, and new pipelines can be added easily by the user.
    - We have also developed a [**web dashboard**](https://digest.neurobagel.org) for interactive visualizations of imaging and phenotypic data availability.

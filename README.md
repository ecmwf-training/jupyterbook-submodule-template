# ECMWF JupyterBook sub-module template

This repository is a GitHub **template** for creating and maintaining a submodule that
can be used in ECMWF Jupyter Books for learning and documentation resources.

## Branch architecture

This template has been designed to be used as a sub-module for a parent repository. Therefore the default branch for this repository is **develop**, and this branch is used to deploy the review/development version of the JupyterBook. The **main** branch is reserved for published content and will be maintained by ECMWF.

The repository includes github-actions which will automatically build a develop version of the Jupyter Book that can be used for review purposes.

### GitHub Actions

:::{note}
This template is designed to be used as a sub-module for a parent repository. The JupyterBook build here is intended for review and testing purposes, and hence the actions are associated to the develop branch. If you are using this repository as a stand-alone JupyterBook you may want to update the default branch and github workflow to use the main branch.
:::

There are two github actions in place for this repository:

#### Build

The **`Build`** action builds the JupyterBook using the same procedure as local build described below. It is activated when a pull request to the `develop` branch is opened, or when any change is made to the develop branch (e.g. after merging a pull request). A pull request can only be merged into the develop branch if the `Build` action is successful.

#### Deploy

The **`Deploy`** action deploys the build JupyterBook to the GitHub Pages associated with this repository. This action is activated when a change is made to the develop branch, after the build action.

## For developers

Clone the repository and create a conda/mamba environment for building Jupyter Books:
```sh
conda create -y -n jupyter-build -c conda-forge python=3.12
conda activate jupyter-build
conda install "jupyter-book>=2,<3"
```

Then build and render the book
```sh
jupyter book clean
jupyter book build
jupyter book start
```
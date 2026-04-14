# ECMWF JupyterBook sub-module template

This repository is a GitHub **template** for creating and maintaining a submodule that
can be used in ECMWF Jupyter Books for learning and documentation resources.

## Adding notebooks and markdown content

If creating a notebook please use the {doc}`./template-notebook` to ensure you
are following the expected guidelines.
Markdown content should follow a similar structure as this README.md file.
To make the added content appear in the Jupyter Book rendered pages, you must add the content to the
table of contents (`toc`) in the `myst.yml` file, e.g.:
```yml
  toc:
    ...
    - my-new-notebook.ipynb
    - my-new-markdown.md
```
Feel free to remove any of the template/placeholder content that is currently listed.


## Branch architecture

This template has been designed to be used as a sub-module for a parent repository.
Therefore the default branch for this repository is **develop**, and this branch is used to
deploy the review/development version of the JupyterBook.
The **main** branch is reserved for published content and will be maintained by ECMWF.

The repository includes github-actions which will automatically build a develop version of
the Jupyter Book that can be used for review purposes.

## GitHub Actions

:::{note}
This template is designed to be used as a sub-module for a parent repository.
The JupyterBook build here is intended for review and testing purposes, and hence
the actions are associated to the develop branch.
:::

There are two github actions in place for this repository:

### Jupyter Book Deploy

The **`Jupyter Book Deploy`** action builds the Jupyter Book using the same procedure as
local build described below then, if action is running on the `develop` branch, the build
is deployed to github pages.
The action is activated or when a change is made to the `develop` branch
(e.g. after merging a pull request) or when a pull request to the `develop` branch is opened.
It can also be triggered manually from the Actions tab in the github page.

### Notebook QA

The **`Notebook QA`** action runs a series of Quality Assessment checks on the notebooks in
the repository. For example the code must meet acceptable coding standards and the notebooks
must run to completion. This check is considered as part of the review process when accepting
new notebooks to the repository.

## Build and check the Jupyter Book locally

Clone the repository and enter the directory:
```sh
git clone git@github.com:ecmwf-training/jupyterbook-submodule-template.git
cd jupyterbook-submodule-template
```

### Create environment and install dependancies for building the Jupyter Book

Create a clean environment using the package manager of your preference,
and install the CI dependencies.
Below are examples for working with `conda` and `uv` package managers.

**conda**:
```sh
# Create and activate a conda environment.
conda create -y -n jupyter-build -c conda-forge python=3.12
conda activate jupyter-build

# Install the depdencies used by jupyterbook build and the notebooks (specified in requirements.txt)
make conda-env-update
```

**uv**:
```sh
# Create and activate a uv virtual environment.
uv venv .venv --python 3.12
source .venv/bin/activate 

# Install the depdencies used by jupyterbook build and the notebooks (specified in requirements.txt)
make uv-env-update
```

### Build and render the book locally

```sh
make jupyter-book
```

You will then be provided with a `localhost` link to view your notebook.

:::{note}
If you have multiple instances of Jupyter Book running on your computer,
the actions may fail as they are not able find an available port to host the
Jupyter Book.
:::

### Run the Notebook QA checks

To run the quality assurance checks, run the following command:

```
make qa
```

:::{note}
The `make qa` command will clone a git repository to a hidden directory (.qa-tools)
and install the dependancies required to execute all the quality assurance checks.
It is recommended that you do this in a virtual environment.
:::


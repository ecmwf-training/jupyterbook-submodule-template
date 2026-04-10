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

## Build the Jupyter Book locally

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

Last updated: 2026-04-09
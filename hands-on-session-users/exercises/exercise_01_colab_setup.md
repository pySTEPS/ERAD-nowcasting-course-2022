# Exercise 1: Install and configure pysteps

In this exercise we install pysteps in Colab. Optionally you can try to install pysteps locally in your computer.

## Setup Colab environment

First you need to login to [Colab](https://research.google.com/colaboratory) and create a new notebook. Installation of the pysteps dependencies can be done by using at least two approaches:

  1. Install all dependencies by using [pip](https://pypi.org/project/pip) (installed in the default Colab environment). This is the safe option that has been thoroughly tested.
  2. Install [conda-colab](https://pypi.org/project/condacolab) and activate the environment by following the instructions at [https://pypi.org/project/condacolab](https://pypi.org/project/condacolab). Then install pysteps dependencies by using [mamba](https://mamba.readthedocs.io/en/latest).

The pysteps dependencies are listed in [environment.yml](https://github.com/pySTEPS/pysteps/blob/master/environment.yml). Install also cartopy because we need it for plotting basemaps in the following exercises.

**NOTE:** When using conda-colab, you need to run the installation block first before running any other blocks. If you try to use the Runtime / "Run all" option to run everything at once, the execution will crash, but the second run will work.

After this, install the [latest development version](https://github.com/pySTEPS/pysteps) of pysteps. Use pip+git, as shown [here](https://www.activestate.com/resources/quick-reads/pip-install-git).

## Download example data

Example datasets are available from the [pysteps data repository](https://github.com/pySTEPS/pysteps-data). Use [pysteps.datasets.download_pysteps_data](https://pysteps.readthedocs.io/en/stable/generated/pysteps.datasets.download_pysteps_data.html) to download the dataset (~323 MB) to your Google Drive.

## Configure pysteps

To allow pysteps to locate the downloaded data, you need to create the pystepsrc file as explained [here](https://pysteps.readthedocs.io/en/stable/user_guide/set_pystepsrc.html). You can use [pysteps.datasets.create_default_pystepsrc](https://pysteps.readthedocs.io/en/stable/generated/pysteps.datasets.create_default_pystepsrc.html#pysteps.datasets.create_default_pystepsrc) to create this file. Then you can use [pysteps.load_config_file](https://pysteps.readthedocs.io/en/stable/generated/pysteps.load_config_file.html#pysteps.load_config_file) to load the configuration.

## Local installation

You can also install pysteps locally in your computer by following [these instructions](https://pysteps.readthedocs.io/en/latest/user_guide/install_pysteps.html). The recommended method is to use conda. Alternatively, you can install the pysteps dependencies in a conda environment by hand and then use the pip+git approach shown above to install the latest version.
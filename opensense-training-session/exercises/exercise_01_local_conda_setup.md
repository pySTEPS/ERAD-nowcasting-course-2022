# Exercise 1: Install and configure pysteps

In this exercise we will install pysteps and its dependencies in a local conda environment. The prerequisite to this approach is that you have Python and package manager conda, mamba or miniforge locally installed. See also [these instructions](TO DO) to install Python and the conda package manager on your machine.

## Installation of pysteps and dependencies in local environment

Make sure you have a Python package manager, such as mamba, micromamba or miniforge. 

Then, in a command prompt or shell, run:

`git clone https://github.com/Deltares-research/pyRainAdjustment.git`

`cd pyRainAdjustment`

`mamba create -n rainadjustment python=3.12 poetry`

`mamba activate rainadjustment`

`poetry install`



## Download example data

Example datasets are available from the [pysteps data repository](https://github.com/pySTEPS/pysteps-data). Use [pysteps.datasets.download_pysteps_data](https://pysteps.readthedocs.io/en/stable/generated/pysteps.datasets.download_pysteps_data.html) to download the dataset (~323 MB) to your Google Drive.

## Configure pysteps

To allow pysteps to locate the downloaded data, you need to create the pystepsrc file as explained [here](https://pysteps.readthedocs.io/en/stable/user_guide/set_pystepsrc.html). You can use [pysteps.datasets.create_default_pystepsrc](https://pysteps.readthedocs.io/en/stable/generated/pysteps.datasets.create_default_pystepsrc.html#pysteps.datasets.create_default_pystepsrc) to create this file. Then you can use [pysteps.load_config_file](https://pysteps.readthedocs.io/en/stable/generated/pysteps.load_config_file.html#pysteps.load_config_file) to load the configuration.

## Local installation

You can also install pysteps locally in your computer by following [these instructions](https://pysteps.readthedocs.io/en/latest/user_guide/install_pysteps.html). The recommended method is to use conda. Alternatively, you can install the pysteps dependencies in a conda environment by hand and then use the pip+git approach shown above to install the latest version.
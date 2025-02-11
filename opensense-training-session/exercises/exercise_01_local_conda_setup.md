# Exercise 1: Install and configure pysteps

In this exercise we will install pysteps and its dependencies in a local conda environment. The prerequisite to this approach is that you have Python and package manager conda, mamba or miniforge locally installed. See also [these instructions](TO DO) to install Python and the conda package manager on your machine.

## Installation of pysteps and dependencies in local environment

Make sure you have a Python package manager, such as mamba, micromamba or miniforge. 

Then, in a command prompt or shell (such as conda prompt or miniforge prompt), run the following steps.

Download the course material to a local folder (do not forget to first change your directory to the folder where you would like to put the course material):
`git clone https://github.com/pySTEPS/ERAD-nowcasting-course-2022.git`

Change directory to the OpenSense Nowcasting workshop material:
`cd ERAD-nowcasting-course-2022`

Now, create a specific Python environment called pysteps:
`mamba create -n pysteps python=3.12 poetry`
or with conda:
`conda create -n pysteps python=3.12 poetry`

Activate the environment:
`mamba activate pysteps`
or with conda:
`conda activate pysteps`

And install pysteps and all dependencies through the `poetry.lock` file that is already in your folder.
`poetry install`


## Check if the installation was successful

### Configure pysteps

To allow pysteps to locate the downloaded data, you need to create the pystepsrc file as explained [here](https://pysteps.readthedocs.io/en/stable/user_guide/set_pystepsrc.html). You can use [pysteps.datasets.create_default_pystepsrc](https://pysteps.readthedocs.io/en/stable/generated/pysteps.datasets.create_default_pystepsrc.html#pysteps.datasets.create_default_pystepsrc) to create this file. Then you can use [pysteps.load_config_file](https://pysteps.readthedocs.io/en/stable/generated/pysteps.load_config_file.html#pysteps.load_config_file) to load the configuration.


## Download example data

Example datasets are available from the [pysteps data repository](https://github.com/pySTEPS/pysteps-data). Use [pysteps.datasets.download_pysteps_data](https://pysteps.readthedocs.io/en/stable/generated/pysteps.datasets.download_pysteps_data.html) to download the dataset (~323 MB) to your Google Drive.



# Exercise 1: Install pysteps

In this exercise we install pysteps in Colab. Optionally you can try to install pysteps locally in your computer.

## Setup Colab environment

First you need to login to [Colab](https://research.google.com/colaboratory) and create a new notebook. Installation of the pysteps dependencies can be done by using at least two approaches:

  1. Install all dependencies by using pip (installed in the default Colab environment).
  2. Install conda-colab and activate the environment by following the instructions at [https://pypi.org/project/condacolab](https://pypi.org/project/condacolab). Then install pysteps dependencies by using [mamba](https://mamba.readthedocs.io/en/latest) (installed in the conda-colab environment).

The dependencies are listed in [environment.yml](https://github.com/pySTEPS/pysteps/blob/master/environment.yml). Install also cartopy because we need it for plotting basemaps in the following exercises.

After this, install the [latest development version](https://github.com/pySTEPS/pysteps/tree/erad2022_short_course_fixes) of pysteps. Use pip+git, as shown [here](https://www.activestate.com/resources/quick-reads/pip-install-git).

## Local installation

You can also install pysteps locally in your computer by following [these instructions](https://pysteps.readthedocs.io/en/latest/user_guide/install_pysteps.html). The recommended method is to use conda. Alternatively, you can install the pysteps dependencies in a conda environment by hand and then use the pip+git approach shown above to install the latest version.
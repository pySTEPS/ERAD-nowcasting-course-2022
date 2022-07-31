# Exercise 2: Read and visualize input data

The purpose of this simple exercise is to download the pysteps example data and read and plot it using the tools implemented in pysteps.

## Download and read the example dataset in Colab

First you need to download an example dataset. The datasets are located in the pysteps data repository: [https://github.com/pySTEPS/pysteps-data](URL). To allow pysteps to locate the downloaded data, you need to create the pystepsrc file explained [here](https://pysteps.readthedocs.io/en/stable/user_guide/set_pystepsrc.html). Choose one dataset ("fmi", "mch", "opera", "knmi", "bom" or "mrms"). For a chosen time, read a time series of at least five observations. Print the metadata.

**Hint:** you can use the utility functions implemented in the [pysteps.datasets](https://pysteps.readthedocs.io/en/stable/pysteps_reference/datasets.html) module.

## Plot the data

The data can then be plotted by using the methods in the [pysteps.visualization](https://pysteps.readthedocs.io/en/stable/pysteps_reference/visualization.html) module. Try different colorscales. Plot the data with a basemap and longitude-latitude lines and labels.

## The following exercises

Choose one dataset (precipitation time series and metadata) and use a variable name that you remember. This will be used in the following exercises.
# Exercise 2: Read, visualize and process input data

The purpose of this exercise is to get the users acquainted with the input data of the nowcasting methods, and its visualization and preprocessing.

## Install pysteps

If you haven't already installed pysteps in your Colab environment, please do so by running [the first notebook](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/block_01_setup.ipynb).

## Download and read the example dataset

First you need to download an example dataset. The datasets are available from the pysteps data repository: [https://github.com/pySTEPS/pysteps-data](URL). To allow pysteps to locate the downloaded data, you need to create the pystepsrc file explained [here](https://pysteps.readthedocs.io/en/stable/user_guide/set_pystepsrc.html). Pick the "fmi" and "mch" datasets that have been tested to work for this exercise. For the mch data, choose the time period between 2015-05-15 15:50-16:50 UTC. For fmi, choose 2016-09-28 14:45-15:50 UTC. Use pysteps functions to read the time series into a numpy array and examine the metadata.

**Hint:** you can use the utility functions implemented in the [pysteps.datasets](https://pysteps.readthedocs.io/en/stable/pysteps_reference/datasets.html) module.

## Visualize the data

The data can be plotted by using the methods in the [pysteps.visualization](https://pysteps.readthedocs.io/en/stable/pysteps_reference/visualization.html) module. Try different colorscales. Plot the data on top of a basemap with longitude-latitude lines and tick labels.

## Try different data processing methods

Pysteps implements various methods for preprocessing the input data. The most important of these include:

| **Functionality**                                              | **Purpose**                                                                                           |
|--------------------------------------------------------------- |-------------------------------------------------------------------------------------------------------|
| upsampling (i.e. reducing spatial resolution)                  | needed for reducing computation time                                                                  |
| picking a smaller subrectangle from the input domain (clipping)| focus to the region of interest to reduce computation time                                            |
| conversion between different units                             | needed, for instance, for converting inputs to rain rate (mm/h, if not already in this unit)          |
| logarithmic transformation of rain rates                       | improve the reliability of optical flow and nowcasting methods                                        |
| normal quantile transformation                                 | needed for transforming the data to normal distribution (if the log-transformation is not sufficient) |

Experiment with the above functionality implemented in the [pysteps.utils](https://pysteps.readthedocs.io/en/stable/pysteps_reference/utils.html) module. When transforming the data values, visualize the transformation and/or analyze the impact on the data distribution.

## Other

Choose one dataset (precipitation time series and metadata) and use variable names that you remember. These will be used in the following exercises.
# Exercise 4: Nowcasting methods - Part 1 deterministic nowcasting

The purpose of this exercise is to illustrate how to construct, visualize and apply verification metrics to a deterministic nowcast using pysteps.

## Import data and perform the pre-processing steps

First we install pysteps and load the example data by running the [helper_input_data](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/helper_input_data.ipynb) notebook. This repeats the basics of exercise 1, 2 and 3. You can run this with the following lines:

```python
from google.colab import drive
import os
# mount the Google Drive folder
# don't attempt to remount if the drive is already mounted
if not os.path.exists("/content/mnt/MyDrive"):
  drive.mount("mnt")
%cd '/content/mnt/MyDrive/Colab Notebooks'
# run the data notebook to load the input dataset
%run helper_nowcasting_methods.ipynb
```

This helper notebook imports the FMI radar data, dBR transforms it and determines the motion field with the Lucas-Kanade optical flow method (see [the notebook of block 3](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/block_03_optical_flow_and_extrapolation.ipynb)). The precipitation data is split in a part for forecasting, called `precip_finite`, which is already dBR transformed and NaN values have been filled with a minimum value, and a part that will be used as observations (`precip_obs`) for model verification of the nowcasts.

The metadata corresponding to `precip_finite` is `metadata_dbr` and the metadata of `precip_obs` is `metadata`.

Finally, the motion field variable is called `motion_field`. You can use these variables in these exercises.

## Deterministic nowcasts

In the deterministic nowcasting part, we will use the loaded data to create a precipitation nowcast and calculate different verification metrics to assess the skill of the nowcast compared to observations.

The first step is to make a nowcast using the **extrapolation** nowcasting method that simply extrapolates the last observed precipitation field along the motion field. You can follow the example in the [PySTEPS example gallery](https://pysteps.readthedocs.io/en/stable/auto_examples/plot_extrapolation_nowcast.html#sphx-glr-auto-examples-plot-extrapolation-nowcast-py). Calculate the nowcasts for 12 leadtimes, i.e. for 1 hour, and visualize some nowcasts with the observations.

The semi-Lagrangian extrapolation method has some keyword arguments that can improve the quality of the nowcast depending on the data. For a full list of the arguments, see the [pySTEPS documentation](https://pysteps.readthedocs.io/en/latest/generated/pysteps.extrapolation.semilagrangian.extrapolate.html).

After creating the nowcast, calculate and visualize the probability of detection (POD), false alarm ratio (FAR), equitable threat score (ETS), and the mean error (ME) for the nowcast as a function of leadtime.

Finally, export the nowcasts into NetCDF format using the `pysteps.io.exporters` module.

If time allows, you can make nowcasts using other methods, for example S-PROG or LINDA (the deterministic version). You can compare the nowcasts visually by plotting them and statistically by calculating the verification metrics for all the nowcasting methods and plotting them in the same figure.

## Visualize the results

Visualize the observations and the nowcasts for a few lead times. An example on how to do this is provided in [the STEPS nowcast gallery example](https://pysteps.readthedocs.io/en/latest/auto_examples/plot_steps_nowcast.html#stochastic-nowcast-with-steps). You can plot the observations on one row and the corresponding nowcasts below them.

## Deterministic nowcast verification

Deterministic nowcasts can be verified with pySTEPS using different kind of metrics: continuous, categorical, spatial and SAL scores.

- `pysteps.verification.detcatscores` contains methods to calculate categorical metrics, i.e. metrics calculated for some rain rate thresholds, for example probability of detection (POD) and false alarm ratio (FAR).
- `pysteps.verification.detcontscores` contains methods to calculate continuous verification metrics, for example mean absolute error (MAE).
- `pysteps.verification.spatialscores` contains methods for calculating the Fractions Skill Score (FSS) and the Binary mean squared error (BMSE).
- `pysteps.verification.salscores` contains methods for calculating the Spatial-Amplitude-Location (SAL) score defined by Wernli et al. (2008)

We will calculate probability of detection (POD), false alarm ratio (FAR), equitable threat score (ETS), and the mean error (ME) for the nowcast as a function of leadtime, and visualize them.

## Exporting nowcasts

Finally, let's export the nowcasts to NetCDF format. For exporting, the exporter needs to first be initialized before it can be used to save the nowcasts. Remember to close the exporter after saving the nowcast.

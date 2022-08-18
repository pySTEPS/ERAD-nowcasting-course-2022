# Exercise 4: Nowcasting methods - Part 2 probabilistic nowcasting
The purpose of this exercise is to illustrate how to construct, visualize and apply verification metrics to a probablistic (ensemble) nowcast using pysteps. 

## Import data and perform the pre-processing steps
First we install pysteps and load the example data by running the [helper_input_data](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/helper_input_data.ipynb) notebook. This repeats the basics of exercise 1, 2 and 3. You can run this with the following lines: 

```
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

This helper notebook imports the FMI radar data, dBR transforms it and determines the motion field with the Lucas-Kanada optical flow method (see [the notebook of block 3](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/block_03_optical_flow_and_extrapolation.ipynb)). The precip data is split in a part for forecasting, called `precip_finite`, which is already dBR transformed and NaN values have been filled with a minimum value, and a part that will be used as observations (`precip_obs`) for model verification of the nowcasts. 

The metadata corresponding to `precip_finite` is `metadata_dbr` and the metadata of `precip_obs` is `metadata`. 

Finally the motion field variable is called `motion_field`. You can use these variables in these exercises.


## Construct the probabilistic nowcasts
In this probabilistic nowcasting part, we will repeat the same basic steps of a deterministic nowcast, but, instead of a deterministic forecast, we will construct and verify a probabilistic STEPS nowcast with 20 ensemble members. If time allows, you can also try to make a LINDA-P nowcast. We can get an estimate of the uncertainty in our forecast with a probabilistic forecast. It can, for instance, tell us what the (forecast) probability is that rainfall above a certain threshold will take place at location *x*. 

The first step is to make a probablistic nowcast using the STEPS approach that is explained in [the STEPS nowcast gallery example](https://pysteps.readthedocs.io/en/latest/auto_examples/plot_steps_nowcast.html#stochastic-nowcast-with-steps). You can follow this example and adjust the code where necessary to make it work for our test case.

Make an ensemble nowcast with 20 ensemble members and 12 lead times of 5 min (one hour in total). You can follow the aforementioned gallery example. For a list of all options when configuring the STEPS nowcast, see the [pysteps documentation](https://pysteps.readthedocs.io/en/latest/pysteps_reference/nowcasts.html#pysteps-nowcasts-steps).

### Visualize the result
Visualize the observations, ensemble mean of the probabilistic nowcast and some individual ensemble members of the nowcast for a few lead times. As a second step, also visualize the probability of exceeding a threshold of 1 mm/h (try some others, too!) for the same lead times. 

An example on how to do this is provided in [the STEPS nowcast gallery example](https://pysteps.readthedocs.io/en/latest/auto_examples/plot_steps_nowcast.html#stochastic-nowcast-with-steps). Start with plotting the observations and continue from there with the other plots below it. 
```
plt.figure(figsize=(16, 16))
# First plot the observations
for i, j in enumerate(range(2, 13, 3)):
    plt.subplot(4, 4, 1 + i)
    plot_precip_field(
        precip_obs[j], 
        geodata=metadata, 
        colorscale="STEPS-BE", 
        colorbar=False
        )
    plt.title(f"Observation at +{(j + 1) * 5} minutes")
```

What can you say about the quality of the forecast and how do the individual ensemble members compare to the ensemble mean?

### Ensemble forecast verification
You have probably seen that the individual ensemble members from the stochastic forecast maintain the same variance as the observed rainfall field. Hence, it gives a less smoothed outcome than the ensemble mean (which looks more like S-PROG in the deterministic nowcast section of this exercise) and also preserves high-intensity rainfall cells. Rainfall forecasts are uncertain on the high spatial and temporal resolution that we want to reach with nowcasting. Therefore, it is highly valuable to take into account an ensemble forecast that provides an estimate of this uncertainty. To verify such an ensemble forecast, it is only fair to use a verification strategy that takes into account the entire ensemble and that threats all members individually. Hence, this verification section will be different from the deterministic nowcast verification. 

Pysteps includes a number of verification metrics to help users to analyze the general characteristics of the nowcasts in terms of consistency and quality (or goodness). In contrast to the verification of the deterministic nowcast, we have a 20-member ensemble that we want to verify. As every member contains valuable information, it is better not to use the deterministic verification metrics on the ensemble mean, but to use a metric that can take the entire ensemble into account. 

Therefore, we will focus on the CRPS (continuous ranked probability score) and we will verify our probabilistic forecasts using the ROC curve, reliability diagrams, and rank histograms, as implemented in the [verification module](https://pysteps.readthedocs.io/en/latest/pysteps_reference/verification.html) of pysteps.

- You can see the [CRPS](https://pysteps.readthedocs.io/en/latest/generated/pysteps.verification.probscores.CRPS.html#pysteps.verification.probscores.CRPS) as the mean absolute error of the ensemble. It compares the cdf of the ensemble with the observed rainfall. Calculate and plot the CRPS for the lead times of your forecast. What do you see?
- Plot the ROC curve, reliability diagram and rank histogram following the [gallery example](https://pysteps.readthedocs.io/en/latest/auto_examples/plot_ensemble_verification.html#sphx-glr-auto-examples-plot-ensemble-verification-py). What can you say about the quality of your ensemble forecast?


## Extra: LINDA-P forecast
If time allows, make a probabilistic LINDA (LINDA-P) forecast using the same forecast settings (12 lead times, 20 ensemble members) as in the previous exercises. The [LINDA gallery example](https://pysteps.readthedocs.io/en/latest/auto_examples/linda_nowcasts.html#sphx-glr-auto-examples-linda-nowcasts-py) will help you to get there!



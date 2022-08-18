# Exercise 4: Nowcasting methods
The purpose of this exercise is to illustrate how to construct, visualize, apply verification metrics to and export a deterministic and probablistic (ensemble) nowcast using pysteps. The exercise starts with some repetition of the previous exercises to make sure that the right data is imported (exercise 1), that the data is transformerd (exercise 2) and that the motion field has been derived for the dataset (exercise 3). Then, we'll start with the construction and verification of deterministic nowcasts, followed by the construction and verification of a probabilistic nowcast.

## Import data
First we install pysteps and load the example data by running the [helper_input_data](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/helper_input_data.ipynb) notebook. This repeats the basics of exercise 1 and 2. You can run this with the following lines: 

```
from google.colab import drive
import os
# mount the Google Drive folder
# don't attempt to remount if the drive is already mounted
if not os.path.exists("/content/mnt/MyDrive"):
  drive.mount("mnt")
%cd '/content/mnt/MyDrive/Colab Notebooks'
# run the data notebook to load the input dataset
%run helper_input_data.ipynb
```

If you still have a running script, you can continue with that. It does not matter from which data provider you have imported the radar data, but *make sure that you have at least 15 time steps available (3 for the nowcasts and advection field derivation and 12 for the observations, which will be used for the forecast verification).*

## Pre-processing steps
We will start with a few pre-processing steps that are the same for the deterministic and probablistic forecasts. These pre-processing steps resemble the steps from exercises 2 and 3 (so you could also continue with your scripts from those exercises). 

### Apply data transformations
The data from FMI has already been imported after running the [helper_input_data](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/helper_input_data.ipynb) notebook. The precip data is called `precip` and the metadata is called `metadata`.

- Index the last 12 timesteps from `precip` and store this as your observations (we will use this during the verification procedure). Keep the remaining timesteps for the motion field derivation and nowcasting.
- Use a dBR transformation (or any [transformation](https://pysteps.readthedocs.io/en/latest/auto_examples/data_transformations.html#sphx-glr-auto-examples-data-transformations-py) you like) to transform the timesteps that will be used for the motion field derviation and nowcasting. 
- If you want to use DARTS (see exercise 3) for the motion field derivation, make sure to set all NaN-values to a minimum value. For instance with: 
```
# Handling of NaN values has been explicitly implemented in Lucas-Kanade and VET,
# but not in DARTS. For this reason, we set all non-finite values to the minimum
# value before applying the optical flow.
precip_finite = precip_dbr.copy()
precip_finite[~np.isfinite(precip_finite)] = np.nanmin(precip_dbr)
``` 

### Determine the motion field
Determine the motion field (pick a method from exercise 3) and visualize it.


## Deterministic nowcasts

To do..

## Probabilistic nowcasts
In probabilistic nowcasting part, we will repeat the basic steps of the deterministic nowcast, but, instead of a deterministic forecast, we will construct and verify a probabilistic nowcast with 20 ensemble members. If time allows, you can also try to make a LINDA-P nowcast. We can get an estimate of the uncertainty in our forecast with a probabilistic forecast. It can, for instance, tell us what the (forecast) probability is that rainfall above a certain threshold will take place at location *x*. 

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


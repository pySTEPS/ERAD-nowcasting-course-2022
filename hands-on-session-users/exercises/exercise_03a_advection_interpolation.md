# Exercise 3 (optional): Precipitation accumulation with advection interpolation

The purpose of this exercise is to demonstrate the advantages of using advection-based temporal interpolation. One of the main applications of this technique is computation of precipitation accumulations, where high temporal resolution is needed.

# Obtain the dataset and compute advection field

Choose a one-hour precipitation rate dataset (13 composites with 5-minute time steps). You can take the one used in [exercise 3](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/exercises/exercise_03_optical_flow_and_extrapolation.md). For computing the advection field, you can also follow that exercise.

# Compute advection-interpolated precipitation fields

Using the above observed precipitation fields, compute a time series where the temporal resolution has been increased to 15 seconds. Use the following approach to interpolate between the observations.

## Description of the interpolation technique

Suppose we are interpolating two precipitation fields P1 and P2 observed at times t1 and t2, to a common time t' in the interval [t1,t2]. In its basic form, the technique has the following steps:

 1. Extrapolate P1 forward and P2 backward to the common time t' by using the [semi-Lagrangian scheme](https://pysteps.readthedocs.io/en/stable/generated/pysteps.extrapolation.semilagrangian.extrapolate.html).
 3. Apply time-weighted linear interpolation between the pixel values of P1' and P2' to obtain the final interpolated field P'.

# Compute accumulated precipitation

Compute hourly precipitation accumulation by using two approaches:

1. The basic approach, where the average precipitation rate (mm/h) of the observations at 5-minute intervals is taken as the hourly accumulation.
2. As above, but by using the interpolated fields to increase the temporal resolution.

Plot the above hourly accumulations side by side and compare the results. What can we see?
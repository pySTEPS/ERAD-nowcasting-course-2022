# Exercise 3: Optical flow and extrapolation

## Install pysteps and download the example dataset

If you haven't already installed pysteps and downloaded the example data, please do so by running the [first](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/block_01_setup.ipynb) and [second](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/block_02_input_data.ipynb) notebooks.

## Try different optical flow methods

Several optical flow methods are implemented in the [pysteps.motion](https://pysteps.readthedocs.io/en/stable/pysteps_reference/motion.html) module. Apply the Lucas-Kanade, VET and DARTS methods to the precipitation time series loaded in the [previous notebook](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/hands-on-users/hands-on-session-users/notebooks/block_02_input_data.ipynb) and measure computation times. Note that the methods have different requirements for the number of input fields (all require at least two).

**Questions:**

- Are data transformations needed or can you apply the methods directly to your data?
- What are the characteristic features the advection field produced by each method? Which one looks the most credible?

Plot the advection fields on top of a precipitation field and a basemap. Do this using the methods implemented in the [pysteps.visualization](https://pysteps.readthedocs.io/en/stable/pysteps_reference/visualization.html) module. Note that plotting the advection field may require adjustment of the default parameters.

## Extrapolate

Apply semi-Lagrangian extrapolation implemented in the [pysteps.extrapolation](https://pysteps.readthedocs.io/en/stable/pysteps_reference/extrapolation.html) module. Use advection field produced by one of the above optical flow methods. Plot the extrapolated precipitation fields for the next 15, 30, 45 and 60 minutes.

By default, the semi-Lagrangian extrapolation produces a time series that has the same time step with the inputs. Use the `timesteps` argument to produce an extrapolated time series for the next 15 minutes with time step of one minute.
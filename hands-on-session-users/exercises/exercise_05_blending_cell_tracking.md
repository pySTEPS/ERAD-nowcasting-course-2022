# Exercise 5: Blending and cell tracking
The purpose of this exercise is to illustrate other forecasting methods that have recently become part of pysteps. You can either work on part A: blending nowcasting with NWP or part B: cell tracking-based nowcasts. If time allows, you can try to do both.

## Part A: Blending with NWP
In this example, we are going to blend a nowcast with an NWP rainfall forecast using three different blending methods, which are implemented in pysteps. Examples of the blending methods are described in [Linear Blending](https://pysteps.readthedocs.io/en/latest/auto_examples/plot_linear_blending.html#sphx-glr-auto-examples-plot-linear-blending-py) and [STEPS blending](https://pysteps.readthedocs.io/en/latest/auto_examples/blended_forecast.html#sphx-glr-auto-examples-blended-forecast-py). We will loosely follow these examples, but for a different dataset from RMI Belgium, which asks for a few more pre-processing steps.

In *helper_blending.ipynb* some first pieces of code are already given to get you started. Furthermore, the examples gallery and your obtained knowledge from the previous exercises should get you there. 

### Install pysteps
If you still have your notebook open, you have already installed pysteps and everything should work. If not, let's first run the first notebook (block 1) to install pysteps and configure it. This is needed because Colab notebooks are independent of each other and it's not possible to save the state of a notebook and use it in another one.

### Load the example dataset

Now that we have initialized the notebook, let's import the example RMI radar and NWP dataset (for a case on 4 July 2021 from 16:05 until 18:00 UTC). To run this, the [pysteps-nwp-importers](https://github.com/pySTEPS/pysteps-nwp-importers) plugin needs to be installed in addition to the pysteps installation. 

### Visualize the data
After importing the data, it is time to inspect it. Plot the radar rainfall field and the first time step of the NWP forecast.
What can you say about the skill of the NWP forecast for this time? How would you blend such a case?

### Reproject NWP data on radar grid
Besides the discrepancy between the NWP forecast for 16:05 UTC and the most recent radar observation for that time, you may have observed that the extent and grid cell size of the NWP forecast is somewhat different than those of the radar observations. A difference with the gallery examples in [Linear Blending](https://pysteps.readthedocs.io/en/latest/auto_examples/plot_linear_blending.html#sphx-glr-auto-examples-plot-linear-blending-py) and [STEPS blending](https://pysteps.readthedocs.io/en/latest/auto_examples/blended_forecast.html#sphx-glr-auto-examples-blended-forecast-py) is that the RMI NWP rainfall forecasts are projected on a different, coarser grid than the RMI radar data. Prior to blending, we will have to reproject the NWP data on the radar grid.

Reproject the NWP data using the [reprojection module](https://pysteps.readthedocs.io/en/latest/pysteps_reference/utils.html?highlight=reprojection#pysteps-utils-reprojection) and visualize the data again. Can you see a difference in the grid extent of the NWP data after reprojection? 

### Linear blending
Let's try out a [Linear Blending](https://pysteps.readthedocs.io/en/latest/auto_examples/plot_linear_blending.html#sphx-glr-auto-examples-plot-linear-blending-py) forecast. in *helper_blending.ipynb* an example is given which resembles the [Linear Blending](https://pysteps.readthedocs.io/en/latest/auto_examples/plot_linear_blending.html#sphx-glr-auto-examples-plot-linear-blending-py) gallery example. Use this code to pre-process, blend and visualize the results and skill of the forecasts. 

What can you say about the blending skill? And what do you think that causes this (hint: think about when the blending takes place, the nowcasting method, etc.)?

Do you think you can improve the blending skill? Play a bit around with the forecast settings and see if and how this improves the forecast. Run two or three new forecasts and visualize the forecast results and skill as before. 

### Salient blending
A disadvantage of simple linear blending is that higher intensity rainfall cells are not preserved, but get smoothed in between the start and end time of the blending procedure. Another option is to use a saliency-based blending method, which focuses more on rainfall intensities over the forecast times, see also [Salient Blending gallery example](https://pysteps.readthedocs.io/en/latest/auto_examples/plot_linear_blending.html#sphx-glr-auto-examples-plot-linear-blending-py) and [Hwang et al., 2015](https://doi.org/10.1175/WAF-D-15-0057.1). The blended product preserves pixel intensities with time if they are strong enough based on their ranked salience. Saliency is the property of an object to be outstanding with respect to its surroundings. The ranked salience is calculated by first determining the difference in the normalized intensity of the nowcasts and NWP. Next, the pixel intensities are ranked, in which equally comparable values receive the same ranking number.

Based on the gallery example and your linear blending approaches, make a saliency-based blending between nowcast and NWP for issue time 16:05 UTC. 
What can you say about the forecast skill compared to linear blending?

### STEPS blending

A disadvantage of the previous methods is that it requires the user to set the start and end time of the blending. The optimal times and blending weights are not known to the user in advance and can change from forecast to forecast. The [STEPS blending method](https://pysteps.readthedocs.io/en/latest/pysteps_reference/blending.html#pysteps-blending-steps) determines the blending weights and timing based on the initial and expected skill of the blending components, which are estimated from the recent and previous skill of the forecast components. The STEPS method, as you have already used for ensemble nowcasts in block 4 of this tutorial, makes it possible to perturb both the nowcast and NWP components on different spatial scale levels, which should lead to a better representation of the uncertainty in the (blended) forecast. 

Use the example code in *helper_blending.ipynb*, the gallery example and your knowledge from the previous steps to create a STEPS blended forecast. Visualize the results and skill again. What can you say about the skill of the blended forecast?

## Part B: Cell tracking
To do..

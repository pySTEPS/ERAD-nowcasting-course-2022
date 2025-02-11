# OpenSense 2025 Training School session

This folder contains the material prepared for the hands-on session on using pysteps with opportunistic sensing data.
The exercises are split into a folder [exercises](opensense-training-session/exercises), containing the description and steps to be taken per exercise, and a folder [notebooks](opensense-training-session/notebooks), which contain the notebooks that can be used for each exercise. The folder [notebooks](opensense-training-session/notebooks) also contains so-called helper scripts, which provide data inputs and pre-processing steps that need to be repeated (e.g. from previous exercises) and can be run directly from the main notebook for that exercise.

**General information**
[TO DO: adjust!]
  * Information about the training school can be found [here](https://indico.scc.kit.edu/event/4626/overview).
  * Flowchart of the session [here](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/session_overview.pdf)
  * The session has some PPT slides: [TO DO, change this] general introduction ([pdf](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/tree/main/hands-on-session-users/slides/introduction.pdf), [pptx](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/tree/main/hands-on-session-users/slides/introduction.pptx)) and introduction & wrapup slides ([pdf](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/tree/main/hands-on-session-users/slides/exercises.pdf), [pptx](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/tree/main/hands-on-session-users/slides/exercises.pptx)) for the exercises.

The exercises are divided into x blocks [TO DO, fill out later - current is copy of ERAD exercices]:

1. Install pysteps and its dependecies
  * In Google Colab: [exercise](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/exercises/exercise_01_colab_setup.md) and [solution 1](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/notebooks/block_01_setup_pip.ipynb)
  * In a local conda or mamba environment: [solution 2](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/notebooks/block_01_setup_conda-colab.ipynb)
2. Read, visualize and process input data: [exercise](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/exercises/exercise_02_input_data.md) and [solution](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/notebooks/block_02_input_data.ipynb)
3. Optical flow and extrapolation: [exercise](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/exercises/exercise_03_optical_flow_and_extrapolation.md) and [solution](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/notebooks/block_03_optical_flow_and_extrapolation.ipynb)
    * Advection interpolation (optional): [exercise](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/exercises/exercise_03a_advection_interpolation.md) and [solution](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/notebooks/block_03a_advection_interpolation.ipynb)
4. Nowcasting methods
    * Deterministic nowcasting: [exercise](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/exercises/exercise_04_deterministic_nowcasting.md) and [solution](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/notebooks/block_04_deterministic_nowcasts.ipynb)
    * Probabilistic nowcasting: [exercise](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/exercises/exercise_04_probabilistic_nowcasting.md) and [solution](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/notebooks/block_04_probabilistic_nowcasts.ipynb)
  5. Blending: [exercise](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/exercises/exercise_05_blending.md) and [solution](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/notebooks/block_05_blending.ipynb)

The attendees are encouraged to try the exercises first before looking at the solutions.

See the README.md files in the [exercises](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/tree/main/hands-on-session-users/exercises) and [notebooks](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/tree/main/hands-on-session-users/notebooks) subfolders.
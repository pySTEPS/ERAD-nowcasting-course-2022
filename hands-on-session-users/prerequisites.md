# Pre-requisites for the “hands-on session” for users

The exercises in this session will be done by using Google Colab notebooks. Therefore the attendees are expected to create a Google account before the session and copy the example notebooks to their Google Drive. The material will be provided in the [GitHub repository](https://github.com/pySTEPS/ERAD-nowcasting-course-2022).

## 1. Create a Google account

If you don't yet have a Google account, create it [here](https://accounts.google.com/signin/v2/identifier?flowName=GlifWebSignIn&flowEntry=ServiceLogin).

## 2. Install Google Chrome

For the best experience, we recommend using [Google Chrome](https://www.google.com/chrome) for this session. In many Linux distributions, the browser is known as [Chromium](https://www.chromium.org/Home), and it can be installed through the distribution's package management system. [Firefox](https://www.mozilla.org), [Microsoft Edge](http://www.microsoft.com/en-us/windows/microsoft-edge) and [Safari](http://www.apple.com/safari) should also work, but they might not support all functionalities needed for using the Google services.

## 3. Clone GitHub Repositories and copy notebooks to Colab

This step is required for running the Colab notebooks shared through the [GitHub repository](https://github.com/pySTEPS/ERAD-nowcasting-course-2022). Sign in to your Google account, go to [Colab](https://colab.research.google.com/?utm_source=scs-index) and run the following commands in a new notebook.

    # mount your Google drive to access it from Colab
    from google.colab import drive
    drive.mount("mnt")
    %cd mnt/MyDrive
    # clone the repository from GitHub
    !git clone https://github.com/pySTEPS/ERAD-nowcasting-course-2022
    # create notebook directory (if it doesn't already exist)
    !mkdir 'Colab Notebooks'
    # copy the course notebooks to the above folder
    # !cp ERAD-nowcasting-course-2022/hands-on-session-users/notebooks/*.ipynb 'Colab Notebooks'

Now you can open the example notebooks in Colab.

## 4. Download example data

Downloading the example data to your Google Drive folder will take some time. To facilitate smooth running of the noteboks, you can do this before the session. The easiest way is to run the [helper notebook](https://github.com/pySTEPS/ERAD-nowcasting-course-2022/blob/main/hands-on-session-users/notebooks/helper_setup_pip.ipynb) made for this purpose.

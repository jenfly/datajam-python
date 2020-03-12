# Computer Setup Instructions

We will be using a program called JupyterLab as our development environment for the workshop. I recommend using Anaconda or Miniconda to install JupyterLab and Python. These are Python distributions which include core Python plus a package manager (`conda`) to manage all the 3rd party libraries you'll need for data analysis.

> Note: Any existing system-wide Python installation on your computer won't be affected by installing Anaconda/Miniconda according to the recommended default settings, as the distribution will be self-contained within your home directory.


Below are a few different options for setting up your laptop. You'll want to have the software installed and working properly before the workshop starts. Sometimes a few minor tweaks are needed to get the software working on different systems, so if you have any problems please email me (jenfly [at] gmail [dot] com) or ask for help at the workshop.


#### Data and Workshop Materials

Please download the [zipped folder of workshop files] and unzip/extract. You can also [view the slides online]. **Coming soon!**

### Step 1: Download and Install

We have three options for this step. Jump to:
- [Option A: Full Anaconda Distribution](#anaconda)
- [Option B: Miniconda](#miniconda)
- [Option C: pip](#pip)

<a id="anaconda"></a>
#### Option A: Full Anaconda Distribution

This option is the easiest to set up and start using. The full Anaconda distribution includes Python, JupyterLab, and hundreds of other popular scientific libraries&mdash;you'll immediately have access to all these libraries without having to find and install them yourself. With this option, you can use the graphical interface (Anaconda Navigator) to launch JupyterLab and manage libraries, or you can work from the command line, if you prefer.


**Download and install Anaconda:** Click the "Download" button under **Python 3.7 version** from the **[Anaconda download page](https://www.anaconda.com/download/)** (the web page should automatically detect your operating system and provide the correct version of the installer with the "Download" button). After it finishes downloading, run the installer, making sure to use all the recommended default settings. We won't be using Microsoft Visual Studio Code, so when the installer asks if you want to install it, you can just click "Skip". For more details on the intallation steps, you can check out the instructions for [Windows](https://docs.anaconda.com/anaconda/install/windows), [Mac](https://docs.anaconda.com/anaconda/install/mac-os), or [Linux](http://docs.anaconda.com/anaconda/install/linux/).

> Note: The Windows installer says 3 GB free space is required, but on my computer I found that the software uses almost double that. These numbers might be a bit different on Mac or Linux.

Next you'll need to do some additional configuration to install the `plotly` library. **[Jump to Step 2](#plotly)**.

<a id="miniconda"></a>
#### Option B: Miniconda

If you want a more minimal installation and are comfortable working from the command line, you can instead install Miniconda, a bare bones version of Anaconda that includes just Python, the `conda` package manager, and a few libraries that `conda` needs. You'll then need to use `conda` to install the other 3rd party libraries that we'll be using in the workshop.

**i) Download and install Miniconda:** Download the **Python 3.7 version** for your operating system from the **[Miniconda download page](https://conda.io/miniconda.html)** and run the installer, making sure to use all the recommended default settings. This installation is much quicker than the full Anaconda distribution and will probably only take a few minutes.

<a id="commandline"></a>

**ii) Check your Miniconda installation:** If you're on Windows, look for a newly installed program called "Anaconda Prompt" and run it to open up a console similar to the screenshot below. If you're on a Mac, look for a program called "Terminal" in the Launchpad, and run it to open a console window.

In either the Windows or the Mac version of the console, type `conda list` and then hit `Enter` to display a list of the currently installed libraries, as in the screenshot.

![Miniconda](img/screenshots/miniconda1.png)

**iii) Install 3rd party libraries:** To install the 3rd party libraries you'll need for the workshop, enter the following command in your console window:
```
conda install jupyterlab numpy pandas matplotlib seaborn ipywidgets
```

Follow the prompts to complete the installation. Then you can run the command `conda list` again in the console, and scroll through the (now much longer) list to confirm that the new libraries have been installed. As you continue to explore Python and want to try out more libraries, you can install them using the `conda install` command in the console.

Next you'll need to do some additional configuration to install the `plotly` library. **[Jump to Step 2](#plotly)**.

<a id="pip"></a>
#### Option C: pip

If you already use `pip` and prefer to use it for package management, go forth and do your thing! You’ll want a Python 3.7 environment with `jupyterlab`, `numpy`, `pandas`, `matplotlib`, `seaborn`, and `ipywidgets`.

Next you'll need to do some additional configuration to install the `plotly` library. Follow the steps below, substituting the appropriate `pip` commands for the listed `conda` commands.

<a id="plotly"></a>
### Step 2: Configuration and Plotly Installation

To use the `plotly` library with JupyterLab, we need to do some additional configuration (same for both Anaconda and Miniconda options).

> The steps below might be a bit tricky, especially if you're not used to working at the command line. If you're having trouble, feel free to skip them and **[jump to Step 3](#step3)**. We can help you with the configuration and `plotly` installation at the workshop.

**i) Update Anaconda/Miniconda libraries:** Open a console window (Anaconda Prompt on Windows / Terminal on Mac), as shown in Option B [above](#commandline). Update all libraries with the command:
```
conda update --all
```

**ii) Install `plotly`:**
```
conda install -c plotly plotly=4.5.2
```

**iii) Install `nodejs`:**
```
conda install -c conda-forge nodejs
```
**iv) Install JupyterLab extensions:** Follow the instructions listed under "JupyterLab Support (Python 3.5+)" in the [Getting Started with Plotly Guide](https://plot.ly/python/getting-started/).

> Note: When following the steps in the Getting Started with Plotly Guide, you don't need to install `jupyterlab` and `ipywidgets` since they're already installed. You can just confirm they are the correct versions with:
```
conda list jupyterlab
conda list ipywidgets
```

<a id="step3"></a>
### Step 3: Test Your Installation

To make sure the software is working properly, we'll open up JupyterLab.

**Option A: Anaconda Navigator:** If you installed the full Anaconda distribution and want to use the graphical interface, look for a newly installed program called "Anaconda Navigator" in your computer's menu, and run it to open up a window similar to the screenshot below. It might take a minute to initialize, and a few other windows might open and close while it's doing so, this is all normal.

Look for the "lab" icon on the Anaconda Navigator dashboard, and click the "Launch" button

![Anaconda Navigator](img/screenshots/navigator.png)

**Option B: Command Line:** To launch JupyterLab from the command line (Anaconda or Miniconda), run the following command in the console window.
```
jupyter lab
```

**JupyterLab:** Whether you launched from Anaconda Navigator or the command line, a new tab should open up in your default web browser, which will look similar to the screenshot below. If so, success!  You're all set! You can start exploring JupyterLab, or just close the browser tab and close the Anaconda Navigator window to exit the program.

<a id="jupyterlab"></a>

![JupyterLab](img/screenshots/jupyterlab.png)



[back to workshop main page](https://jenfly.github.io/datajam-python/)

# FibPhoFlow

FibPhoFlow is an open-source fiber photometry data analysis package compatible with data obtained from [TdT fiber photometry](https://www.tdt.com/system/behavior-and-fiber-photometry/) hardware and software.

## Installation

This package is currently available on PyPi for download with pip, but certain dependency issues associated with the HDF5 data storage related python packages, h5py and pytables, tend to cause build errors in different environments. The simplest way to use this python package is to use the python package manager, Anaconda. If you are trying to pip install this package without Conda you will need to download the C package HDF5. https://www.hdfgroup.org/downloads/hdf5/.

### Step 1: 
- Download [Anaconda](https://www.anaconda.com/download) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html)
- Download an IDE which allows you to see plots, such as [Spyder](https://www.spyder-ide.org/) or [Jupyterlab](https://jupyter.org/)
  - You can install Spyder or Jupyterlab once you have Conda with:
    ```conda install -c anaconda spyder```
    ```conda install -c conda-forge jupyterlab```

### Step 2: Create Conda virtual environment for fibphoflow
- Open your [Terminal](https://cs.colby.edu/maxwell/courses/tutorials/terminal/)
- Create a folder on your desktop to launch Conda environment
```
mkdir folder_name
cd folder_name
```
- Right click save this Anaconda virtual environment (venv) file into this folder
```https://raw.githubusercontent.com/nikhayes/fibphoflow/main/src/environment.yml```
- While in the folder you created, create the Conda venv (includes needed package dependences)
```conda env create -f environment.yml```
- Activate Conda venv
```conda activate fibphoflow_venv```
- For more information on general conda venv usage, [see here](environments.html#activating-an-environment)

### Step 3: Connect the Conda venv with your IDE
- Configure your venv with Spyder or Jupyter [with these instructions](https://medium.com/@apremgeorge/using-conda-python-environments-with-spyder-ide-and-jupyter-notebooks-in-windows-4e0a905aaac5)

## Overview of Workflow

* Note that a well documented practice analysis walkthrough will be added soon.

1. The raw fiber photometry data streams from TdT photometry recording directories are loaded using the TdT python package. TdT recording files need to be located in the working directory or its subdirectories for them to be located while running fibphoflow.py. The script is currently only compatible with a GCaMP and UV/Isosbestic stream.

2. A simple low pass filtering step (a moving average) is applied to help smooth out signal noise

3. The streams (GCaMP and UV) are downsampled based on the hz value one sets.

4. A normalization of the calcium stream is performed using the isosbestic stream

5. From here, based on the experimental metadata found in the experiment's excel file, the processed streams from step 3 are chopped up into specific "epoch" traces for analysis and these traces are normalized to user-defined recording baseline periods to obtain traces in terms of delta F/F.


## To-do's

1. Fix package dependency issues and allow for download with conda-forge

2. Add option for butterworth low pass filtering step.

3. Make things more Jupyter compatible so that report printouts can be made easier

4. Clean up code commenting/documentation, along with error messages

5. Add third red calcium channel

6. Add z-scoring
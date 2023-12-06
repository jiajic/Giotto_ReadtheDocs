====================================================
Resolve Biosciences Molecular Cartography Human Lung
====================================================

:Date: Compiled 2023-07-14

.. container:: cell

   .. code:: r

      # Ensure Giotto Suite is installed.
      if(!"Giotto" %in% installed.packages()) {
        devtools::install_github("drieslab/Giotto@Suite")
      }

      library(Giotto)
      # Ensure the Python environment for Giotto has been installed.
      genv_exists = checkGiottoEnvironment()
      if(!genv_exists){
        # The following command need only be run once to install the Giotto environment.
        installGiottoEnvironment()
      }

1 Set up Giotto environment
===========================

.. container:: cell

   .. code:: r

      # 1. ** SET WORKING DIRECTORY WHERE PROJECT OUPUTS WILL SAVE TO **
      results_folder = '/path/to/save/directory/'

      # 2. set giotto python path
      # set python path to your preferred python version path
      # set python path to NULL if you want to automatically install (only the 1st time) and use the giotto miniconda environment
      python_path = NULL 
      if(is.null(python_path)) {
        installGiottoEnvironment()
      }

      # 3. Create Giotto instructions
      # Directly saving plots to the working directory without rendering them in the editor saves time.
      instrs = createGiottoInstructions(save_dir = results_folder,
                                        save_plot = TRUE,
                                        show_plot = FALSE,
                                        return_plot = FALSE)

2 Dataset Explanation
=====================

This vignette covers Giotto object creation and simple exploratory
analysis with Resolve Biosciences’ *Molecular Cartography* platform data
using their `Human Lung
dataset <https://resolvebiosciences.com/open-dataset/?dataset=human-lung-dataset>`__.
The data from sample **873_C1** will be worked with.

3 Project data
==============

| Please first download all the data for sample sample **873_C1** into a
  common directory and then specify that directory below.
| A set of segmentations data was not found at the time of this writing,
  so we provide segmentations generated using StarDist and QuPath using
  the `dsb2018_heavy_augment.pb
  model <https://github.com/qupath/models/tree/main/stardist>`__.

.. container:: cell

   .. code:: r

      # data directory
      mc_dir = '/path/to/molecular_cartography/data/directory'

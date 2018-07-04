This is an urbansim-2 implementation of the PSRC land use model. It is a python package that contains PSRC-specfic modifications to the urbansim package developed by Synthicity.

It's under construction. Currently, only a simple version of the real estate price model (REPM) is implemented.

**Requirements:**

1. Install Anaconda Python: http://continuum.io/downloads
#. Install the UDST packages urbansim and urbansim_defaults: https://github.com/UDST
#. Set the environmental variable PYTHONPATH to point to those directories.
#. Create a base year dataset as an hdf5 file, e.g. by running the script data/create_base_year.py. It converts csv files into hdf5.
#. Set the environmental variable DATA_HOME to the directory with your base year dataset (minus the 'data' subdirectory). The code will look for the data file in $DATA_HOME/data.

To estimate, run the estimate.py script. The configuration of the REPM can be found in configs/repm.yaml. 

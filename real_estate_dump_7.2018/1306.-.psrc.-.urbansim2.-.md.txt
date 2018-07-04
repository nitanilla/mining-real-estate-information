# PSRC UrbanSim

[![Travis-CI Build Status](https://travis-ci.org/psrc/urbansim2.svg?branch=master)](https://travis-ci.org/psrc/urbansim2)
[![Coverage Status](https://coveralls.io/repos/github/psrc/urbansim2/badge.svg?branch=master)](https://coveralls.io/github/psrc/urbansim2?branch=master)

This is an urbansim-2 implementation of the PSRC land use model. It is a python package that contains PSRC-specfic modifications to the urbansim package developed by UrbanSim Inc. (former Synthicity). 


## Installation

### Setup:

In the examples below it will be assumed that the base directory for the installation is ``d:/udst``.


1. Install [Anaconda Python](http://continuum.io/downloads), the latest of the 2.* series (not 3.*). By default it will be installed in a different directory than existing Python, so there is no danger in messing up the current Python installation. Alternatively, use a virtual enviornment specific for Urbansim2. In a command prompt, start a new virtual environment called "urbansim2" as follows:

```
conda create -n urbansim2 python=2.7 anaconda
```
Activate this environment every time you restart the prompt and want to work with urbansim2 by entering the follow (for Windows prompts):

```
activiate urbansim2
```

(In a bash shell, type "source activate urbansim2".)

In addition to Anaconda Python, two other packages (zbox and prettytable) are needed. Install using the following pip commands:
   
   ```
   pip install zbox
   pip install prettytable
   ```
   
2. Clone this repository into a directory called ``psrc_urbansim``:
   
   ```
   cd /d/udst
   git clone https://github.com/psrc/urbansim2.git psrc_urbansim
   ```
   
3. Install the UDST packages ``urbansim``, ``urbansim_defaults``, ``orca`` and ``pandana`` by cloning them from [UDST GitHub](https://github.com/UDST):

   ```
   cd /d/udst
   git clone https://github.com/UDST/urbansim.git urbansim
   git clone https://github.com/UDST/urbansim_defaults.git urbansim_defaults
   git clone https://github.com/UDST/orca.git orca
   git clone https://github.com/UDST/pandana.git pandana
   git clone https://github.com/UDST/developer.git developer
   git clone https://github.com/UDST/choicemodels.git choicemodels
   ```
   
4. Set the environment variable PYTHONPATH to point to those directories, as well as this repository, ``psrc_urbansim``. If you plan to switch between Opus and UrbanSim-2, put these settings into a  file that can be executed prior to working in the UrbanSim-2 environment. E.g. create a file ``setpath.bat`` with 

   ```
   SET PYTHONPATH=D:/udst/psrc_urbansim;D:/udst/urbansim;D:/udst/urbansim_defaults;D:/udst/orca;D:/udst/pandana
   ```
   
   If you prefer to work with Git Bash, you can put something like this into a file called ``setpath.sh``:
   
   ```
   DIR=/d/udst
   export PYTHONPATH=$DIR/psrc_urbansim:$DIR/urbansim:$DIR/urbansim_defaults:$DIR/orca:$DIR/pandana
   ```
   
5. Set the PATH variable to point to the Anaconda directory. E.g. add this line to the ``setpath.bat`` file:
   
   ```
   SET PATH=c:/Anaconda;c:/Anaconda/Scripts;%PATH%
   ```
   
   or in bash:
   
   ```
   export PATH=/c/Anaconda:/c/Anaconda/Scripts:$PATH
   ```
    
6. Create a base year dataset as an hdf5 file by running the script [``psrc_urbansim/data/conversion/cache_to_hdf5.py``](https://github.com/psrc/urbansim2/tree/master/data/conversion/cache_to_hdf5.py) (see [more info](https://github.com/psrc/urbansim2/tree/master/data/conversion)). Move the resulting file into ``psrc_urbansim/data``.
7. Set the environment variable ``DATA_HOME`` to the directory with your base year dataset (minus the ``data`` subdirectory). The code will look for the data file in $DATA_HOME/data. E.g. add this line to ``setpath.bat``:
 
   ```
   SET DATA_HOME=D:/udst/psrc_urbansim
   ```
   
   or in bash:
   
   ```
   export DATA_HOME=$DIR/psrc_urbansim
   ```

8. Put the name of the data file into ``psrc_urbansim/configs/settings.yaml`` (node ``store``).

### Code Update

The code is evolving fast, so update it regularly.

```
cd /d/udst/urbansim
git pull
git pull psrcedits dev
cd ../orca
git pull
cd ../pandana
git pull
cd ../urbansim_defaults
git pull
git pull psrcedits dev
```

This can be automated as has been done on modelsrv3, see the next section.

### Setup Note for modelsrv3

On modelsrv3, the packages are already installed, as well as the baseyear data is available. To update the code, open a Git Bash and do:

```
cd /d/udst
./update_all.sh
```

The script iterates over the packages and pulls from the corresponding repositories.

To set the environment variables in step 4, 5 and 7, depending where you want to run UrbanSim-2:

1. **Windows command line:** Open a terminal, go into the ``d:/udst`` directory and do:

   ```
   setpath.bat
   ```
 
2. **Git Bash**: Open a Git Bash window and do 
 

   ```
   cd /d/udst
   source setpath.sh
   ```

In both cases, it changes the environment only for the session in this terminal or bash window.

The base year data are stored in ``/d/udst/psrc_urbansim/data/psrc_base_year_2014.h5``.


## Using UrbanSim-2

The code is under construction. Currently, only a prototype of the model system is implemented. One can estimate the real estate price model, household location choice model and job location choice model. A simulation script is also available. 

### Estimation

Model estimation is controlled from the file ``estimate.py``. In that file, uncomment a line corresponding to the model to be estimated. For example, for estimating residential real estate price model, make sure the line  

```
orca.run(["repmres_estimate"])
```

is uncommented, while all other lines except imports are commented out. Then run 

```
python estimate.py
```

The UI of the various models is implemented in ``psrc_urbansim/models.py``. For the example above, we'll find the following section in the ``models.py`` file:

```
@orca.step('repmres_estimate')
def repmres_estimate(parcels):
    return utils.hedonic_estimate("repmres.yaml", parcels, None)
```

This tells us that the model is using a specification defined in the file  ``configs/repmres.yaml``. Note that this file is used as an input as well as output, so the estimation results can be found there. New variables should be implemented in the directory ``psrc_urbansim/vars``, depending on the corresponding dataset. 



### Simulation

A simulation can be started from the file ``simulate.py``. Here, uncomment all models you want to run and define the set of simulation years. Outputs will be written into a file defined in the argument ``data_out``.

```
python simulate.py
```


## Pushing Changes to GitHub

For now, since everything is under development, we will push all our changes into the master branch (unless you want to have your own experimental branch). 

### Exclusions

There are a few files that are either automatically overwritten by the estimation procedure (e.g. yaml config files) or that have temporary changes not to be committed (e.g. estimate.py, simulate.py) and thus, we want them to be excluded from commits. There are bash scripts in the main directory that can help with that. First check with ``git status`` if some of these "unwanted" files are in line for a commit. If it is the case, BEFORE you run commit, you can use (from a bash terminal):

* ``source gitexclude_yaml.sh``: excludes all yaml files found in the configs directory.
* ``source gitexclude.sh filename``: excludes a specific file given by the filename.
* ``source gitinclude.sh filename``: includes a previously excluded file given by the filename. 

Then run commit and push. For example, you made changes in the HLCM specification that should be committed, but you also ran test estimations of other models results of which should not be pushed to GitHub, neither the estimate.py file. In such a case, you can do:

```
source gitexclude_yaml.sh
source gitinclude.sh configs/hlcm.yaml
source gitexclude.sh estimate.py
git status
git commit -am 'describe your changes'
git push
```

The first line excludes all yaml files while the second line "unexcludes" hlcm.yaml and the third line adds the estimate.py file to the exclusions. Always check with ``git status`` that it is doing what you want.

### Merging

If you excluded a file and somebody else makes changes to it that collide with yours, the ``git pull`` command will most likely throw an error. There are various ways to deal with it depending on if you want to keep your changes or not. For keeping your changes look at the [git stash documentation](https://git-scm.com/book/en/v1/Git-Tools-Stashing). If you want to throw your changes away, do 

```
git checkout filename
```

with filename being the file you want to overwrite.

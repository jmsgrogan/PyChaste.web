---
layout: page-full-width
title: Installation
---

## Quickstart - Python

### Linux

The easiest way to get started is with [Anaconda](), which allows easy installation of a range of scientific Python packages in binary form.

If you already have `conda` just do:

    conda config --add channels conda-forge
    conda config --add channels jmsgrogan
    conda install microvessel-chaste

and you are ready to go. Run `microvessel-chaste notebooks` in a shell to see a selection of demo Jupyter notebooks in your web browser.

To quickly install the neccessary  [Anaconda]() software you can do:

    wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh
    chmod 777 Miniconda2-latest-Linux-x86_64.sh
    ./Miniconda2-latest-Linux-x86_64.sh
    conda update conda

and follow the install instructions.

TODO: Docker instructions

### Windows/MacOS

It is best to use [Docker](), a lightweight container similar to a virtual machine, on these platforms. Install Docker according to the [instructions for your OS](https://docs.docker.com/).

TODO: Instructions for adding docker channel and launching notebooks in browser.

## Build From Source (Linux) - C++ and Python

If you would like to start using or customizing the C++ solvers you need to build from source. This is reasonably straightforward.

First, Chaste dependencies need to be built following the [Chaste Install Guide](https://chaste.cs.ox.ac.uk/trac/wiki/InstallGuides/InstallGuide). 

The project only supports the development version of Chaste. This can be obtained by doing:

    git clone -b develop https://chaste.cs.ox.ac.uk/git/chaste.git $CHASTE_SOURCE_DIR

The project code itself can be obtained by doing: 

    git clone https://github.com/jmsgrogan/MicrovesselChaste.git $MICROVESSEL_PROJECT_SOURCE_DIR

The Microvessel project code needs to be included in the main Chaste source. This can be done with a symbolic link:

    cd $CHASTE_SOURCE_DIR/projects
    ln -s $MICROVESSEL_PROJECT_SOURCE_DIR

The C++ libraries can be built using the [Chaste CMake build system](https://chaste.cs.ox.ac.uk/trac/wiki/ChasteGuides/CmakeBuildGuide). First, create a build directory outside the source tree and proceed as:

    cd $CHASTE_BUILD_DIR
    cmake $CHASTE_SOURCE_DIR
    make project_MicrovesselChaste -j $NUM_AVAILABLE_CPUS

This will build the C++ library and all tests. To avoid building tests do:

    make chaste_project_MicrovesselChaste -j $NUM_AVAILABLE_CPUS

as the final command. The [Chaste CMake build system guide](https://chaste.cs.ox.ac.uk/trac/wiki/ChasteGuides/CmakeBuildGuide) should be consulted for options related to generating optimized builds, running other types of test and installation as a system library.

To build the Python library it is neccessary to first build [PyChaste](), a Python wrapper for Chaste. Do: 

    git clone https://github.com/jmsgrogan/PyChaste.git $PYCHASTE_PROJECT_SOURCE_DIR
    cd $CHASTE_SOURCE_DIR/projects
    ln -s $PYCHASTE_PROJECT_SOURCE_DIR
    cd $CHASTE_BUILD_DIR
    cmake $CHASTE_SOURCE_DIR
    make chaste_project_PyChaste -j $NUM_AVAILABLE_CPUS
    make chaste_project_PyChaste_Python -j $NUM_AVAILABLE_CPUS
    cd $CHASTE_BUILD_DIR/projects/PyChaste/python/chaste
    python setup.py install

Similarly, for Microvessel Chaste do:

    cd $CHASTE_BUILD_DIR
    make project_MicrovesselChaste_Python -j $NUM_AVAILABLE_CPUS
    cd $CHASTE_BUILD_DIR/projects/MicrovesselChaste/python/microvessel-chaste
    python setup.py install

You can then import `chaste` and `microvessel-chaste` in a Python session.


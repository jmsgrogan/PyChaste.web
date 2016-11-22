---
layout: page-full-width
title: Installation
---

## Linux

### Conda Package

The [conda](https://www.continuum.io/downloads) package is recommended. If you already have `conda` installed just do:

    conda config --add channels conda-forge
    conda config --add channels jmsgrogan
    conda install chaste

You should then be able to do:

    import chaste

in a python session. 

If you need to install `conda`, the [Miniconda](http://conda.pydata.org/miniconda.html) package will suffice. 

### Docker

A Docker image is also available. This image will launch a Jupyter notebook at [htpp://localhost::8888](htpp://localhost::8888) in a web browser, which can be used to try out the package. If you already have docker installed do:

    docker pull jmsgrogan/pychaste
    docker run -it -p 8888:8888 pychaste

and go to the above link in your browser.

To install Docker follow the [instructions here](https://docs.docker.com/).

## Windows/MacOS

### Docker

Only Docker is supported on these platforms at the moment. Install Docker following the [instructions here](https://docs.docker.com/) and proceed as per the Linux Docker instructions above.


## Build From Source (Linux Only)

It is reasonably straightforward to build the package from source on Linux.

First, Chaste dependencies need to be built following the [Chaste Install Guide](https://chaste.cs.ox.ac.uk/trac/wiki/InstallGuides/InstallGuide). 

The project only supports the development version of Chaste. This can be obtained by doing:

    git clone -b develop https://chaste.cs.ox.ac.uk/git/chaste.git $CHASTE_SOURCE_DIR

The project code itself can be obtained by doing: 

    git clone https://github.com/jmsgrogan/PyChaste.git $PYCHASTE_PROJECT_SOURCE_DIR

The wrapper code needs to be included in the main Chaste source. This can be done with a symbolic link:

    cd $CHASTE_SOURCE_DIR/projects
    ln -s $PYCHASTE_PROJECT_SOURCE_DIR

The Python modules can be built using the [Chaste CMake build system](https://chaste.cs.ox.ac.uk/trac/wiki/ChasteGuides/CmakeBuildGuide). First, create a build directory outside the source tree and proceed as:

    cd $CHASTE_BUILD_DIR
    cmake $CHASTE_SOURCE_DIR
    make chaste_project_PyChaste -j $NUM_AVAILABLE_CPUS
    make chaste_project_PyChaste_Python -j $NUM_AVAILABLE_CPUS
    cd $CHASTE_BUILD_DIR/projects/PyChaste/python/chaste
    python setup.py install

You can then import `chaste` in a Python session.

The [Chaste CMake build system guide](https://chaste.cs.ox.ac.uk/trac/wiki/ChasteGuides/CmakeBuildGuide) should be consulted for options related to generating optimized builds.

## Troubleshooting

* Missing Boost Python when building from source: If you are building from source you may need to install Boost Python in addition to the Chaste dependencies. Do `sudo apt-get install libboost-python-dev` on Ubuntu to obtain it.
* Missing librt.so when loading conda package: this is a problem with the version of VTK in conda-forge. Make sure you have added the conda channels in the order above.
* Missing liblapack.so when loading conda package: libatlas is needed on the system. Do `sudo apt-get install libatlas-base-dev` on Ubuntu.


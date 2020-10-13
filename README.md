Tasks
=====

[![License](https://img.shields.io/badge/License-BSD%202--Clause-green.svg)](https://opensource.org/licenses/BSD-2-Clause)
[ ![Download](https://api.bintray.com/packages/gergondet/multi-contact/Tasks%3Amulti-contact/images/download.svg) ](https://bintray.com/gergondet/multi-contact/Tasks%3Amulti-contact/_latestVersion)
[![CI](https://github.com/jrl-umi3218/Tasks/workflows/CI%20of%20Tasks/badge.svg?branch=master)](https://github.com/jrl-umi3218/Tasks/actions?query=workflow%3A%22CI+of+Tasks%22)
[![Documentation](https://img.shields.io/badge/doxygen-online-brightgreen?logo=read-the-docs&style=flat)](http://jrl-umi3218.github.io/Tasks/doxygen/HEAD/index.html)

Tasks is library for real time control of robots and kinematic trees using constrained optimization.
It has been used extensively to control humanoid robots such as HOAP-3, HRP-2, HRP-4 and Atlas.

Documentation
-------------

Features:
 * Support Kinematics Tree with Revolute/Prismatic/Spherical/Free/Planar/Cylindrical joints
 * Dynamic motion (motion must fulfill the equation of motion)
 * Contact forces in friction cones
 * Static contacts
 * Articular position, speed and torque limits
 * Collision avoidance
 * Multi-robot contact (can solve problems involving multiple robots in contact)
 * Tasks:
  * Posture target (articular position target, mandatory if you want avoid singularity issues)
  * Link Position/Orientation target
  * Link Velocity target
  * Center of Mass (CoM) target
  * Momentum target
  * Contact force target

To make sure that Tasks works as intended, unit tests are available for each algorithm.

The [SpaceVecAlg and RBDyn tutorial](https://github.com/jorisv/sva_rbdyn_tutorials) is also a big resources to understand how to use Tasks by providing a lot of IPython Notebook that will present real use case.

An online documentation can be found [online](https://jrl-umi3218.github.io/Tasks).

Installing
----------

## Ubuntu LTS (16.04, 18.04, 20.04)

```bash
# Make sure you have required tools
sudo apt install apt-transport-https lsb-release ca-certificates gnupg
# Add our key
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key 892EA6EE273707C6495A6FB6220D644C64666806
# Add our repository (stable versions)
sudo sh -c 'echo "deb https://dl.bintray.com/gergondet/multi-contact-release $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/multi-contact.list'
# Use this to setup the HEAD version
# sudo sh -c 'echo "deb https://dl.bintray.com/gergondet/multi-contact-head $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/multi-contact.list'
# Update packages list
sudo apt update
# Install packages
sudo apt install libtasks-dev python-tasks python3-tasks
```

## Conan

Install the latest version using [conan](https://conan.io/)

```bash
conan remote add multi-contact https://api.bintray.com/conan/gergondet/multi-contact
# Install the latest release
conan install Tasks/latest@multi-contact/stable
# Or install the latest development version
# conan install Tasks/latest@multi-contact/dev
```

## Homebrew OS X install

Install from the command line using [Homebrew](brew.sh):

```bash
# install homebrew package manager
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# install caskroom application manager
brew install caskroom/cask/brew-cask
# tap homebrew-science package repository
brew tap homebrew/science
# tap ahundt-robotics repository
brew tap ahundt/robotics
# install tasks and all its dependencies
brew install tasks
```

## Manually build from source

### Dependencies

To compile you need the following tools and libraries:

 * [Git]()
 * [CMake]() >= 2.8
 * [pkg-config]()
 * [doxygen]()
 * [g++]() >= 4.7 (for C++11 support)
 * [Boost](http://www.boost.org/doc/libs/1_58_0/more/getting_started/unix-variants.html) >= 1.49
 * [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) >= 3.2
 * [SpaceVecAlg](https://github.com/jrl-umi3218/SpaceVecAlg)
 * [RBDyn](https://github.com/jrl-umi3218/RBDyn)
 * [eigen-qld](https://github.com/jrl-umi3218/eigen-qld)
 * eigen-lssol (Optional, if you have the LSSOL licence ask us this library)
 * [sch-core](https://github.com/jrl-umi3218/sch-core)

For Python bindings:
 * [Cython](http://cython.org/) >= 0.2
 * [Eigen3ToPython](https://github.com/jrl-umi3218/Eigen3ToPython)
 * [sch-core-python](https://github.com/jrl-umi3218/sch-core-python)

### Building

```sh
git clone --recursive https://github.com/jrl-umi3218/Tasks
cd Tasks
mkdir _build
cd _build
cmake [options] ..
make && make intall
```

#### CMake options

By default, the build will use the `python` and `pip` command to install the bindings for the default system version (this behaviour can be used to build the bindings in a given virtualenv). The following options allow to control this behaviour:

 * `PYTHON_BINDING` Build the python binding (ON/OFF, default: ON)
 * `PYTHON_BINDING_FORCE_PYTHON2`: use `python2` and `pip2` instead of `python` and `pip`
 * `PYTHON_BINDING_FORCE_PYTHON3`: use `python3` and `pip3` instead of `python` and `pip`
 * `PYTHON_BINDING_BUILD_PYTHON2_AND_PYTHON3`: builds two sets of bindings one with `python2` and `pip2`, the other with `python3` and `pip3`
 * `BUILD_TESTING` Enable unit tests building (ON/OFF, default: ON)

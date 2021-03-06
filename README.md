# Tesseroids: forward modeling of gravitational fields in spherical coordinates

by [Leonardo Uieda](http://www.leouieda.com/),
[Valéria C. F. Barbosa](http://lattes.cnpq.br/0391036221142471),
and [Carla Braitenberg](http://www.lithoflex.org)

This repository contains the manuscript and supplementary code and data for a
paper about the open-source software package
[Tesseroids](http://tesseroids.leouieda.com).  It also describes an optimal
method for modeling gravitational fields due to spherical prism mass elements
(tesseroids).

The *Tesseroids* software is written in the C programming language and has no
external dependencies (other than a C compiler).  The error analysis presented
in the paper was performed using Python code to run the C programs, examine the
output, and generate plots.

**The manuscript has been published in the journal
[Geophysics](http://library.seg.org/journal/gpysa7) on the September-October
2016 issue**.

doi:[10.1190/geo2015-0204.1](http://dx.doi.org/10.1190/geo2015-0204.1)

Archived PDF of the article:
[leouieda.com/papers/paper-tesseroids-2016.html](http://www.leouieda.com/papers/paper-tesseroids-2016.html)

Please cite it as:

> Uieda, L., V. Barbosa, and C. Braitenberg (2016), Tesseroids: Forward-modeling gravitational fields in spherical coordinates, GEOPHYSICS, F41–F48, doi:10.1190/geo2015-0204.1.

You will find the C source-code for Tesseroids and the contents of this
repository at [software.seg.org](http://software.seg.org).
A "live" version of this repository is available at
[github.com/pinga-lab/paper-tesseroids](https://github.com/pinga-lab/paper-tesseroids).

![Figure showing the adaptive discretization method](https://raw.githubusercontent.com/pinga-lab/paper-tesseroids/master/figs/tesseroid-split.png)

## Abstract

We present the open-source software Tesseroids, a set of command-line programs
to perform the forward modeling of gravitational fields in spherical
coordinates.  The software is implemented in the C programming language and
uses tesseroids (spherical prisms) for the discretization of the subsurface
mass distribution.  The gravitational fields of tesseroids are calculated
numerically using the Gauss-Legendre Quadrature (GLQ).  We have improved upon
an adaptive discretization algorithm to guarantee the accuracy of the GLQ
integration.  Our implementation of adaptive discretization uses a "stack"
based algorithm instead of recursion to achieve more control over execution
errors and corner cases.  The algorithm is controlled by a scalar value called
the distance-size ratio (D) that determines the accuracy of the integration as
well as the computation time.  We determined optimal values of D for the
gravitational potential, gravitational acceleration, and gravity gradient
tensor by comparing the computed tesseroids effects with those of a homogeneous
spherical shell.  The values required for a maximum relative error of 0.1% of
the shell effects are D = 1 for the gravitational potential, D = 1.5 for the
gravitational acceleration, and D = 8 for the gravity gradients.  Contrary to
previous assumptions, our results show that the potential and its first and
second derivatives require different values of D to achieve the same accuracy.
These values were incorporated as defaults in the software.


## Reproducing the results

The [Jupyter (formerly IPython) notebooks](http://jupyter.org/) located in the
`notebooks` directory of this repository generate all data, results, and
figures in this paper.  They run the command-line programs and contain all
Python source used to analyze the results and produce figures.  The notebooks
also contain supporting text that explains each step of the process.

The notebooks use the Tesseroids command-line programs, the geophysics Python
library [Fatiando a Terra](http://fatiando.org), and libraries from the [Scipy
ecosystem](http://scipy.org/) to perform the calculations and generate figures.
Data generated by the notebooks is stored in the `data` directory.

**You do not need IPython to view the contents of the notebooks**. If you have
a C compiler and access to Python 2.7 and the required well established
libraries, you should be able to run the code presented in the notebooks with
slight modifications.  The only parts that will require modifications are the
ones that run the C-coded command-line programs. IPython provides a shortcut to
run shell commands in the notebook. Any line that starts with `!` is
interpreted as a bash shell command. This shortcut can be mixed with the rest
of the Python code, like for loops, making it much easier than traditional
shell scripting. If the reader wants to reproduce this code without IPython,
the `!` lines can be replaced by calls to the `subprocess` module from the
Python standard library without much effort.

**Note to Windows users**: the notebooks make heavy use of bash shell commands
to run the *Tesseroids* programs. The notebook that performs the calculations
will require that you have bash installed to run. The figure generation
notebooks should work without modifications or bash. A way to install a bash
environment in Windows is through the [Git for Windows project](https://git-for-windows.github.io/).
Make sure to run to the notebook server (`jupyter notebook`) inside a bash
shell.

You can view a static (not executable) version of the notebooks as PDF files in
the `notebooks` folder or from the [nbviewer](http://nbviewer.ipython.org/) web
service (links below):

* [Figures for the Methodology section](http://nbviewer.ipython.org/github/pinga-lab/paper-tesseroids/blob/master/notebooks/methods_figures.ipynb)
* [Results and preliminary figures for comparison with a spherical shell](http://nbviewer.ipython.org/github/pinga-lab/paper-tesseroids/blob/master/notebooks/tesseroid_vs_spherical_shell.ipynb)
* [Final version of results figures for the article](http://nbviewer.ipython.org/github/pinga-lab/paper-tesseroids/blob/master/notebooks/results-figures.ipynb)

If you have IPython installed, see below for instructions on running the code
in the notebooks.

### Getting the files

To actually run the code in the notebooks, you'll need to have the files on
your machine. You can download a [zip archive of this
repository](https://github.com/pinga-lab/paper-tesseroids/archive/master.zip)
to get everything. A snapshot of this repository is also available as part of
the Geophysics article at [software.seg.org](http://software.seg.org).

### Installing the software

First, you'll need to download the Tesseroids v1.2 software.  You can get the
source code and compiled binaries from:

* The official site: http://tesseroids.leouieda.com
* Zenodo: http://dx.doi.org/10.5281/zenodo.16033
* The official archived version that accompanies the Geophysics paper at
  [software.seg.org](http://software.seg.org).

The Zenodo DOI and software.seg.org links take you directly to version 1.2 and
should be available even if the official site goes offline.

After downloading, unpack the executables (or compile the code) and place them
somewhere included in your PATH environment variable (so that your terminal or
`cmd.exe` can find them).

Next, you'll need to install Python and the required libraries to execute the
Jupyter (IPython) notebooks.  The easiest way to get Python and all libraries
installed is through the [Anaconda Python
distribution](http://continuum.io/downloads).  Be sure to select the **Python
2.7** version of Anaconda.  After you've installed Anaconda, install the
libraries by running the following command in your terminal:

    conda install numpy scipy jupyter matplotlib mayavi pillow pandas basemap

The `requirements.txt` file details the specific versions of these libraries
that were used to produce the results of this paper.

After Anaconda, you'll need to install the geophysics library [Fatiando a
Terra](http://www.fatiando.org) version 0.3.  You can do this by running the
following command in your terminal:

    pip install fatiando==0.3

**Note to Windows users**: See the
[documentation of Fatiando a Terra](http://fatiando.github.io/v0.3/install.html)
for extra software you'll need.

### Running the notebooks

Once the software is installed, you must start an notebook server to run the
code in the notebooks.  Do this by typing in a terminal (or `cmd.exe` in
Windows):

    jupyter notebook

This should open an Internet browser tab with a page to navigate your computers
folders.  Go to where you saved the `notebooks` folder on your computer and
click on the notebook file you want to run.  You can execute the code cells by
clicking on one and typing `Shift+Enter`.  Be sure to execute the code cells in
descending order to get the correct results.  Some cells may take a long time
to run, particularly those that calculate the tesseroid fields.

## License

All source code is made available under a BSD 3-clause license.  You can freely
use and modify the code, without warranty, so long as you provide attribution
to the authors.  See `LICENSE.md` for the full license text.

The manuscript text is not open source. The rights to the article content are
reserved to the journal Geophysics, where it has been accepted for publication.

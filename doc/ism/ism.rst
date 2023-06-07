ISM hands-on
============

You can download the exercises into your Sciserver image or in a directory on your laptop from Github::

  user@linux:~> git clone https://github.com/summerschool-ahead2020/ism-hands-on.git
  
In the `Renkulab image <https://renkulab.io/projects/j.de.plaa/ahead2020-school-spex/sessions>`_, the files 
should already be there in the ``notebooks/ism-hands-on/`` directory.

SPEX and the instellar medium
-----------------------------

In general, the interstellar medium can be modelled by two SPEX models.
The Hot model, for gas at different temperatures and the Amol dust model.

Hot SPEX gas model
''''''''''''''''''

The hot model calculates the transmission of a plasma in collisional ionisation equilibrium with cosmic abundances.
It includes both continuum and line opacity. The model allows you to change the temperature and the column density.
Usually most of the gas along the line of sight can be fit by a neutral (cold) plasma. This cold gas can be mimicked
by setting the default temperature to 1E-3 eV (1 x 10\ :sup:`-6` keV). In this case we freeze the temperature.
In case of warmer or hot gas along the line of sight we set the temperature to thawn.

AMOL SPEX dust model
''''''''''''''''''''

In order to study the dust in the spectra of X-ray binaries we want to analyze the dust with a dedicated model.
This model is called amol and contains the edges of lab measurements of interstellar dust analogues,
which were converted to interstellar dust models. The SPEX manual contains a list of dust models, each of them has
a unique number, which can be set in the amol model (``i1, ..., i4``). The amol model allows for a maximum of four
different dust species to be fitted at the same time. The column densities of these dust models can be set with
``n1, ..., n4``.

Exercises
---------

Exercise 1: Fitting the dust in the X-ray binary of GX 17+2
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Data files: gx17/GX_17.res gx17/GX_17.spo

In this example we use the spectrum of GX 17+2 to test the amol model and to try and fit the Si K-edge.
We first import numpy and matplotlib and define a function which enables us to plot the photon flux.

See the Jupyter notebook (``fit_gx17_example2.ipynb``) in the root of the directory ``ism-hands-on``.


Exercise 2: Future XRISM observations of an X-ray binary: Fe K edge
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

In order to study the dust in the spectra of X-ray binaries we want to analyze the dust with a dedicated model.
This model is called ``amol`` and contains the edges of lab measurements of interstellar dust analogues,
which were converted to interstellar dust models.

In this example we use the spectrum of an X-ray binary on high extinction sightline to explore the possibilities
of XRISM by investigating the Fe K edge.

See the Jupyter notebook (``xrism_sim.ipynb``) in the root of the directory ``ism-hands-on``.


Exercise 3: Fitting ISM dust and multi-temperature gas along the line of sight of an X-ray binary
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

In this exercise we will fit simulated XMM RGS data of the X-ray binary 4U 1820-30. We will use it to fit
different gas components along the line of sight.

This folder contains XMM RGS data of the X-ray binary 4U 1820-30. Let us try to fit several components of
the ISM with different temperatures. For more inspiration check `Costantini et al. 2012
<https://ui.adsabs.harvard.edu/abs/2012A%26A...539A..32C/abstract>`_ or `Rogantini et al. 2021
<https://ui.adsabs.harvard.edu/abs/2021A%26A...645A..98R/abstract>`_.

The filenames are ``xrism-sim-xraybinary/simxmm2.res`` and ``xrism-sim-xraybinary/simxmm2.spo``.

Use the following settings to start::

    s.dist(1,7.6,'kpc')
    s.com('bb)
    s.com('comt')
    s.com('hot') 
    s.com('amol')
    s.com('hot') 
    s.com('hot') 

Relate the models!::

    s.par(1,1,'t',0.14)
    s.par(1,1,'norm',5e-5)
    s.par(1,2,'norm',2.0)
    s.par(1,2,'t0',0.32) 
    s.par(1,2,'t1',29)
    s.par(1,2,'tau',3) 

These are useful dust models for amol::

    s.par(1,4,'i1',3302)
    s.par(1,4,'i2',4103)


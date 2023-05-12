SPEX introduction
=================

SPEX is a spectral fitting program used to fit high-resolution X-ray
spectra. The code contains several simple and detailed models that are
able to deal with the radiative processes observed in the X-ray band.

SPEX has both a command-line and a Python interface. This chapter
provides some basic commands and threads to fit X-ray
spectra from Python. Alternatively, you could read the
`Introduction to the SPEX command-line interface
<https://spex-xray.github.io/spex-help/getstarted/runspex.html>`_.

The SPEX data format
--------------------

The data files containing the spectrum of the source and the response
need to be in the correct format. In the SPEX installation, we provide a
program called `trafo <https://spex-xray.github.io/spex-help/getstarted/runtrafo.html>`_
to convert OGIP standard fits files into SPEX format. There is also a Python
based alternative called `ogip2spex <https://spex-xray.github.io/pyspextools/tutorials/ogip2spex.html>`_.
In this chapter, we assume that you already have spectra in SPEX
format provided by the exercises. Each exercise contains a ``.spo`` and ``.res``
file that can be downloaded from this site.

SPEX needs two files per spectrum:

-  ``<filename>.spo`` – This file contains the countrate per energy bin
   for the source (D\ :sub:`i`\ ), as well as the background countrate and
   the errors (σ\ :sub:`i`\ ).

-  ``<filename>.res`` – This file contains the instrumental response:
   the energy redistribution and effective area (R\ :sub:`ij`\  A\ :sub:`j`\ ).

In order to calculate the observed model spectrum, SPEX uses this
integral equation to account for the imperfections caused by the
instrument:

- D(c) =  ∫ R(c,E) A(E) S(E) dE

- D\ :sub:`i`\ =  Σ\ :sup:`n` :sub:`j=1` R\ :sub:`ij`\ A\ :sub:`j`\ S\ :sub:`j`


The ``.res`` and ``.spo`` files are so-called FITS files. This is a data
format widely used in Astronomy. FITS files can contain images as well
as data tables. The software package `FTOOLS
<https://heasarc.gsfc.nasa.gov/ftools/>`_ provided by NASA contains a
large number of tools to manipulate FITS files. If you
are interested, then you can launch ``flaunch`` to see which tools are
available.

Starting SPEX in Python/Jupyter
-------------------------------

Before you continue, please make sure that you have downloaded the
files from `<https://github.com/summerschool-ahead2020/spex-hands-on>`_
using git as described on the page above.

The ``intro`` directory that you downloaded using git, contains a
``SPEX_Intro.ipynb`` file. You can open this notebook to get a SPEX
demonstration in Python.

When the SPEX package is installed and loaded in the environment successfully,
the notebook should be able to run. Below, we walk through the commands
step-by-step to explain what we do.

In a Python or Jupyter session, SPEX can be started like this::

    >>> from pyspex.spex import Session
    >>> s=Session()
    Welcome user to SPEX version 3.07.03
    ...
    >>>

The object `s` now contains the SPEX program. Through `s` we can send commands
to SPEX and sometimes get data in return. The commands are very similar to the
commands used on the SPEX command line.

As a first step, we can load the data files. This is done using the `s.data()
<https://spex-xray.github.io/spex-help/pyspex/com_data.html#data>`_ command.
The command first expects the response file (with the `.res` extension) and
then the spectrum file (`.spo` extension). In the intro directory we have a
file called ``powerl.spo`` and ``powerl.res``. To load them, you type::

   >>> s.data("powerl.res","powerl.spo")

The responsefile (.res) is entered first and then the file containing
the spectrum (.spo). Remember that the order of the words in the
commands is very important!

Plotting the data
-----------------

If the `s.data() <https://spex-xray.github.io/spex-help/pyspex/com_data.html#data>`_
command was successful, we can now have a look at the
spectra. Using default settings, the easiest way of plotting a spectrum is
as follows::

   >>> s.plot_data()

The command above opens a Matplotlib window and tells SPEX that we
want to plot the spectral data (`s.plot_data()
<https://spex-xray.github.io/spex-help/pyspex/com_plot.html#plot-data>`_).
This will create a linear-linear plot in keV units.

The plot can be tailored to your wishes. Below is an example to create a
plot to a log-log plot in Å::

   >>> s.plot_data(xlog=True, ylog=True, wave=True)

To make sure the axes are logarithmic, we provide the options (``xlog=True`` and
``ylog=True``) and change the axes to unit Å using ``wave=true``.

If you want to change more features of the plot, you can get the
matplotlib ``plt`` object from the command like this::

    >>> (pdata, plt) = s.plot_data(show=False)

The ``pdata`` object contains an astropy table with the plot data, while the
``plt`` object contains the matplotlib.pyplot object. You can use this plt object to
change plot features, for example::

    >>> plt.xlim(xmin, xmax)
    >>> plt.ylim(ymin, ymax)

To change the reach of the x and y axes. You can use all the available
matplotlib.pyplot commands to modify your plot and finally show it with
the ``plt.show()`` command.

Ignoring and rebinning
----------------------

High-resolution X-ray spectra from Chandra and XMM-Newton are usually
oversampled (e.g. the energy bins are much smaller than the spectral
resolution) and contain a lot more channels then is useful. Therefore,
it is necessary to remove wavelength intervals which contain bad data
and rebin your spectrum. The SPEX command to ignore parts of the spectrum
is called `s.ignore() <https://spex-xray.github.io/spex-help/pyspex/com_data.html#data-selection>`_
and the command to rebin is called `s.bin()
<https://spex-xray.github.io/spex-help/pyspex/com_data.html#binning-and-data-selection>`_.
In the next example we bin the spectrum over the 0.5 to 10 keV range with
a factor of 5 and ignore the rest of the spectrum::

   >>> s.ignore(1, 1, 0.0, 0.5, unit='kev')
   >>> s.ignore(1, 1, 10.0, 1000., unit='kev')
   >>> s.bin(1, 1, 0.5, 10.0, 5, unit='kev')

The `s.ignore() <https://spex-xray.github.io/spex-help/pyspex/com_data.html#data-selection>`_
and `s.bin() <https://spex-xray.github.io/spex-help/pyspex/com_data.html#binning-and-data-selection>`_
commands need to know which spectrum in the
data structure you want to change. If you just loaded one spectrum, this is
easy. SPEX organizes spectra in instruments and regions. The first spectrum
is by default in instrument 1 and region 1. The first two places in the
`s.ignore() <https://spex-xray.github.io/spex-help/pyspex/com_data.html#data-selection>`_
and `s.bin() <https://spex-xray.github.io/spex-help/pyspex/com_data.html#binning-and-data-selection>`_
commands need to contain the instrument number and
the region number of the spectrum that you want to change.

The third and forth number is the energy range to apply the command to. So,
the third number is the minimum energy and the forth the maximum.

For the bin command, the binning factor is the fifth entry. Finally, we
provide the unit of our energy values as ``unit='kev'`` in the last entry
of the command.

Defining a model
----------------

Now we have a clean and rebinned spectrum that is ready to fit. Before
we can start fitting, we first need to define a model. It’s equivalent
to :math:`S(E)` in Eq. :eq:`eq_data`. The model can contain
one or more of these components:

-  ``absm`` Model for interstellar absorption.

-  ``reds`` Redshift.

-  ``po`` Powerlaw.

And `there are more <https://spex-xray.github.io/spex-help/models.html>`_!
The following command sequence defines a simple powerlaw model at a certain
redshift and absorbed by the interstellar medium. The individual components
of the model are loaded one-by-one with the `s.com()
<https://spex-xray.github.io/spex-help/pyspex/com_model.html#components>`_ command::

   >>> s.com('reds')
   >>> s.com('absm')
   >>> s.com('po')
   >>> s.com_rel(1,3,numpy.array([1,2]))

The last command (`s.com_rel(1,3,numpy.array([1,2]))
<https://spex-xray.github.io/spex-help/pyspex/com_model.html#component-relate>`_)
tells SPEX that component 3, the powerlaw, is first redshifted by component 1
and then absorbed by component 2. The order of the 1 and the 2 is
important! Always think what happens in which order on the way from
the source to the telescope.

Distance
~~~~~~~~

For most sources the distance is more or less known. To get a right
luminosity estimate for the source, the expected distance has to be
provided to SPEX. This is done with the `s.distance()
<https://spex-xray.github.io/spex-help/pyspex/com_model.html#distance>`_
command::

   >>> s.dist(1, 0.1, 'z')

With this command, the distance to the source is set to a redshift of
0.1.

Setting initial parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~

Now we have to estimate the initial parameters. With the command
`s.par_show() <https://spex-xray.github.io/spex-help/pyspex/com_model.html#show-parameters>`_
we can see which parameters there are::

    >>> s.par_show()
    ----------------------------------------------------------------------------------
    sect comp mod  acro parameter with unit     value      status    minimum   maximum

      1    1 reds z    Redshift              0.000000     frozen   -1.0      1.00E+10

      1    2 absm nh   Column (1E28/m**2)   9.9999997E-05 thawn     0.0      1.00E+20
      1    2 absm f    Covering fraction     1.000000     frozen    0.0       1.0

      1    3 pow  norm Norm (1E44 ph/s/keV)  1.000000     thawn     0.0      1.00E+20
      1    3 pow  gamm Photon index          2.000000     thawn    -10.       10.
      1    3 pow  dgam Photon index break    0.000000     frozen   -10.       10.
      1    3 pow  e0   Break energy (keV)   1.0000000E+10 frozen    0.0      1.00E+20
      1    3 pow  b    Break strength        0.000000     frozen    0.0       10.
      1    3 pow  type Type of norm          0.000000     frozen    0.0       1.0
      1    3 pow  elow Low flux limit (keV)  2.000000     frozen   1.00E-20  1.00E+10
      1    3 pow  eupp Upp flux limit (keV)  10.00000     frozen   1.00E-20  1.00E+10
      1    3 pow  lum  Luminosity (1E30 W)   1.000000     frozen    0.0      1.00E+20

    --------------------------------------------------------------------------------
    Fluxes and restframe luminosities between   2.0000     and    10.000     keV

    sect comp mod   photon flux   energy flux nr of photons    luminosity
               (phot/m**2/s)      (W/m**2)   (photons/s)           (W)
       1    3 pow    0.00000       0.00000       0.00000       0.00000

We can set the parameters using the `s.par()
<https://spex-xray.github.io/spex-help/pyspex/com_model.html#setting-parameters>`_
command. The commands then look like this::

   >>> s.par(1, 1, 'z', 0.1)
   >>> s.par(1, 2, 'nh', 2.E-3, thawn=False)
   >>> s.par(1, 3, 'norm', 1.E+10, thawn=True)
   >>> s.par(1, 3, 'gamm', 1.5, thawn=True)

When the parameter should be free during the fit, then add the optional ``thawn=True`` parameter
to the command. Then, we run `s.par_show() <https://spex-xray.github.io/spex-help/pyspex/com_model.html#show-parameters>`_
again to see what happened::

   >>> s.par_show()
   ----------------------------------------------------------------------------------
   sect comp mod  acro parameter with unit     value      status    minimum   maximum

      1    1 reds z    Redshift              0.100000     frozen   -1.0      1.00E+10

      1    2 absm nh   Column (1E28/m**2)   2.0000001E-03 thawn     0.0      1.00E+20
      1    2 absm f    Covering fraction     1.000000     frozen    0.0       1.0

      1    3 pow  norm Norm (1E44 ph/s/keV)  1.000000E+10 thawn     0.0      1.00E+20
      1    3 pow  gamm Photon index          1.500000     thawn    -10.       10.
      1    3 pow  dgam Photon index break    0.000000     frozen   -10.       10.
      1    3 pow  e0   Break energy (keV)   1.0000000E+10 frozen    0.0      1.00E+20
      1    3 pow  b    Break strength        0.000000     frozen    0.0       10.
      1    3 pow  type Type of norm          0.000000     frozen    0.0       1.0
      1    3 pow  elow Low flux limit (keV)  2.000000     frozen   1.00E-20  1.00E+10
      1    3 pow  eupp Upp flux limit (keV)  10.00000     frozen   1.00E-20  1.00E+10
      1    3 pow  lum  Luminosity (1E30 W)  5.6014867E+08 frozen    0.0      1.00E+20

   --------------------------------------------------------------------------------
   Fluxes and restframe luminosities between   2.0000     and    10.000     keV

    sect comp mod   photon flux   energy flux nr of photons    luminosity
               (phot/m**2/s)      (W/m**2)   (photons/s)           (W)
       1    3 pow    0.00000       0.00000       0.00000       0.00000

Finding the right initial values for the parameters is a game of trial
and error. To see whether you are going in the right direction, you can
calculate the model with the command `s.calc()
<https://spex-xray.github.io/spex-help/pyspex/com_model.html#calculate>`_ and
see the result with `s.plot_data() <https://spex-xray.github.io/spex-help/pyspex/com_plot.html#plot-data>`_.
If you see the model appear in your screen, then the model
is close enough to be fitted. Especially the normalization of the powerlaw
(``norm``) can vary a lot depending on the count rate of the source.

Fitting the data
----------------

We are ready to fit the data! You can give the `s.fit()
<https://spex-xray.github.io/spex-help/pyspex/com_opt.html#fit>`_ command to
start fitting. When the fit is done, then the parameters and C-stat are
printed on screen. If the C-stat value is
close to the expected C-stat value, then your fit is acceptable.
Sometimes more runs of the command `s.fit()
<https://spex-xray.github.io/spex-help/pyspex/com_opt.html#fit>`_ are
necessary after changing some initial parameters. This is especially true
when using complex models. Again this is a game of trial and error::

    >>> s.fit()

You also might want to fix or free certain parameters to see if they can
be constrained. You can fix a parameter with the command `s.par_fix
<https://spex-xray.github.io/spex-help/pyspex/com_model.html#fix-free-parameters>`_ and
freeing is done with `s.par_free() <https://spex-xray.github.io/spex-help/pyspex/com_model.html#fix-free-parameters>`_
(thawn). For example, you can free the N\ :sub:`H` by the following command::

   >>> s.par_free(1,2,'nh')

Calculating errors
------------------

When the fit is acceptable, you might want to know the uncertainties on
your fitted parameters. Errors are determined one-by-one by fixing the
parameter to some value and calculate the ΔC-stat with
respect to the best fit. If you want to know the 1σ error
on the parameter, you need to know its values at ΔC-stat = 1.
This is done by the `s.error
<https://spex-xray.github.io/spex-help/pyspex/com_opt.html#error>`_ command. You
can calculate the error for each parameter. For example gamma::

   >>> gamm_err = s.error(1,1,'gamm')

The result of the error calculation is stored in the
[gamm_err](https://spex-xray.github.io/spex-help/pyspex/optimize.html#error-calculation) object.

Checking your result
--------------------



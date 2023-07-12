Fit a powerlaw with a Gaussian line in SPEX
===========================================

Instructions
------------

The files :download:`powgaus.spo <powgaus.spo>`
and :download:`powgaus.res <powgaus.res>` contain an absorbed
powerlaw spectrum with a Gaussian line. From an optical observation of
the source we know that this source has a redshift of *z* =
0.0345. There is also Galactic foreground absorption. The source has
been observed with the same instrument as the previous exercise.

#. Load the spectrum into SPEX, select the proper energy range and rebin
   the spectrum properly. Set up a model with the right components (a
   gaussian is added with the command ``s.com('gaus')``) and fit the
   spectrum.

#. You may want to fit first with the line flux set to zero (freeze or
   fix some parameter of the line, make a fit, and then fine-tune the
   line by releasing the relevant parameters.

   Read the section in the SPEX manual about `Fluxes and Luminosities
   <https://spex-xray.github.io/spex-help/pyspex/com_model.html#flux-luminosity>`_
   and learn how you can set the energy limits with ``s.elim()`` and
   how to get the fluxes with ``s.flux_get()``. The definition of the
   output can be found `on this page
   <https://spex-xray.github.io/spex-help/pyspex/model.html#fluxes-and-luminosities>`_.

#. What is the 2–10 keV luminosity of the source? What is the difference
   between absorbed and unabsorbed flux?

#. What is the energy of the centroid of the line? Calculate the
   equivalent width of the line using Python. (Equivalent width is defined as
   the ratio between the line flux and the flux of the continuum in the band
   around the line). You can use the fluxes provided by the ``s.flux_get()``
   command if you choose the energy limits well. What is the unit of
   equivalent width?

#. Calculate the errors on all free parameters. What is the error in the
   equivalent width that you calculated?

Learning goals
--------------

After having done this spectrum, you should know:

-  How to make complex spectral models.

-  How to freeze or thaw parameters (using `s.par_fix() and s.par_free()
   <https://spex-xray.github.io/spex-help/pyspex/com_model.html#fix-free-parameters>`_)

-  How to obtain fluxes & luminosities (using `s.flux_get() and s.elim()
   <https://spex-xray.github.io/spex-help/pyspex/com_model.html#flux-luminosity>`_)

-  How to calculate the equivalent width of a line and its error.

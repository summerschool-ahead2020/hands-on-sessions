Fit a power law in SPEX
=======================

The spectrum in the files :download:`powerl.spo <powerl.spo>`
and :download:`powerl.res <powerl.res>` was recorded
from a source at 6 kpc distance.

#. Load the spectrum into PYSPEX and plot it.

#. The calibration of the instrument is not very accurate for energies
   below 0.3 keV and above 10 keV. Ignore those parts of the spectrum.

#. How many data bins do you have in the spectrum? Now try to apply
   optimal binning to the spectrum. How many bins are left?

#. Set up an absorbed powerlaw model. Do not forget to set the distance
   to the source.

#. Next step: fit the spectrum. Is it a good fit?

#. Calculate the errors on all free parameters and save your results in
   a python variable.

**Learning goals:**

After having done this spectrum, you should know:

-  How to read a spectrum in SPEX (using `s.data()
   <https://spex-xray.github.io/spex-help/pyspex/com_data.html#data>`_).

-  How to use the basic plot functionalities (using `s.plot_data()
   <https://spex-xray.github.io/spex-help/pyspex/com_plot.html#plot-data>`_).

-  How to ignore parts of the spectrum (using `s.ignore()
   <https://spex-xray.github.io/spex-help/pyspex/com_data.html#data-selection>`_).

-  How to optimally bin a spectrum (using `s.obin()
   <https://spex-xray.github.io/spex-help/pyspex/com_data.html#binning-and-data-selection>`_).

-  How to set-up a simple spectral model (using `s.com() and s.com_rel()
   <https://spex-xray.github.io/spex-help/pyspex/com_model.html#components>`_).

-  How to set the distance (using `s.dist()
   <https://spex-xray.github.io/spex-help/pyspex/com_model.html#distance>`_).

-  How to do spectral fitting (using `s.fit()
   <https://spex-xray.github.io/spex-help/pyspex/com_opt.html#fit>`_).

-  How to determine errors on parameters (using `s.error()
   <https://spex-xray.github.io/spex-help/pyspex/com_opt.html#error>`_).


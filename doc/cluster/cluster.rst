
Cluster hands-on
================

The hands-on session will be dedicated to the analysis of XMM-Newton/EPIC-PN data on the famous galaxy cluster Abell 1689. We will start by fitting XMM-Newton spectra from this observation using the Python implementation of *XSPEC*. If there is enough time, we will proceed with the analysis of the radial profiles of this system in order to determine its total and baryonic masses.

Unfortunately SciServer does not seem to work for the purpose of this tutorial. For the people who would need an alternative, I have prepared a session on RenkuLab

Spectral fitting: Renku setup
-----------------------------

Create an account on Renku by visiting the following website

`https://renkulab.io <https://renkulab.io/>`_

.. image:: renku_login.png
   :width: 40pt

Once you have created an account, visit the `page of the project <https://renkulab.io/projects/dominique.eckert/galaxy-cluster-profiles>`_
and click *Start* on the top-right corner.

After the session has started, open a Terminal from the dashboard and run the following command::

    pip install -r requirements.txt

The data are pre-loaded into the session in the *A1689* subdirectory. In there you will find a notebook entitled *A1689_spectral_analysis.ipynb*, double click on the file to open the notebook.


Spectral fitting: Laptop setup
------------------------------

If you wish to run this part on your own laptop, make sure HEASOFT is properly installed and loaded, and *PyXSPEC* is accessible. To test for this, run::

    python -c "import xspec"

To download the data package, open a Terminal and run::

    mkdir A1689
    cd A1689
    wget https://www.isdc.unige.ch/~deckert/A1689_spectral_fitting.tar.gz
    tar xvf A1689_spectral_fitting.tar.gz







Cluster hands-on
================

The hands-on session will be dedicated to the analysis of XMM-Newton/EPIC-PN data on the famous galaxy cluster Abell 1689. We will start by fitting XMM-Newton spectra from this observation using the Python implementation of *XSPEC*. If there is enough time, we will proceed with the analysis of the radial profiles of this system in order to determine its total and baryonic masses.

Unfortunately SciServer does not seem to work for the purpose of this tutorial, as the APEC installation in the HEASARC image is incomplete. For the people who would need an alternative, I have prepared a session on `Renku <https://renkulab.io/>`_

Renku setup
-----------

Create an account on Renku by visiting the following website

`https://renkulab.io <https://renkulab.io/>`_

.. image:: renku_login.png
   :width: 400pt

Once you have created an account, visit the `page of the project <https://renkulab.io/projects/dominique.eckert/galaxy-cluster-profiles>`_
and click *Start* on the top-right corner.

After the session has started, open a Terminal from the dashboard and run the following command::

    pip install -r requirements.txt


Laptop setup
------------

If you wish to run this part on your own laptop, make sure HEASOFT is properly installed and loaded, and *PyXSPEC* is accessible. To test for this, run::

    python -c "import xspec"

To download the data package, open a Terminal and run::

    git clone https://renkulab.io/gitlab/dominique.eckert/galaxy-cluster-profiles.git
    cd galaxy-cluster-profiles
    source load_packages.sh

The last command will create a new conda environment entitled *pymc* which will contain the required packages and will be visible from Jupyter Lab. Start a new Jupyter server and select the *pymc* kernel.

Accessing the data and the exercises
------------------------------------

If you use Renku, the data are pre-loaded into the session in the *A1689* subdirectory. On your laptop, you will find the same data under the *A1689* subdirectory of the package download via git.

In there you will find two notebooks:

- *A1689_spectral_analysis.ipynb*: analysis of XMM-Newton spectra of A1689
- *A1689_Mass_modeling.ipynb*: modeling the mass profile of A1689

Double click on the files to open them.

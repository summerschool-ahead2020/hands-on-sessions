Software installation
=====================

Sciserver setup (recommended)
-----------------------------

Create a HEASOFT image on Sciserver as explained on `the HEASOFT Sciserver documentation
page <https://heasarc.gsfc.nasa.gov/docs/sciserver/>`_. We have tested the exercises with HEASOFT 6.31.1.

Creating a conda environment for SPEX on Sciserver
''''''''''''''''''''''''''''''''''''''''''''''''''

Once you have the Jupyterlab environment running on Sciserver, write the following commands in the terminal::

    (heasoft) idies@aaaa:~$ conda activate base
    (base) idies@aaaa:~$ conda create -n spex python=3.9 astropy matplotlib ipykernel
    (base) idies@aaaa:~$ conda activate spex
    (spex) idies@aaaa:~$ conda install -c spexxray spex pyspextools
    (spex) idies@aaaa:~$ python -m ipykernel install --user --name spex --display-name "(spex)"


Laptop setup (advanced)
-----------------------

It is also possible to install the needed software on your own laptop. This takes a bit more work and problems can
occur. Therefore, we recommend to use the Sciserver environment if you do not have a lot of experience with installing
software.

.. warning:: There will NOT be a lot of time to help people with installation problems at the school. Make sure
             that you have at least the Sciserver option running (see above). If you want to run the software on
             your own laptop, then make sure that you do the installation and solve the problems in the week before
             the school starts!

During the school, we will use the following software packages:

  - HEASOFT (version >=6.31), with Hitomi and Xspec packages.
  - SPEX (version 3.07.03).

Install HEASOFT
'''''''''''''''

For the school, you need a recent version of HEASOFT (preferably >=6.31) with at least the Hitomi software and Xspec
installed. See the `HEASOFT download page <https://heasarc.gsfc.nasa.gov/docs/software/lheasoft/download.html>`_
for download and install instructions for your machine. Make sure that you check at least the boxes for Hitomi and
Xspec when you install (downloading more packages is recommended).

Install the HITOMI CALDB
''''''''''''''''''''''''

In addition, you would need to download the `HITOMI SXS calibration files
<https://heasarc.gsfc.nasa.gov/FTP/caldb/data/hitomi/sxs/goodfiles_hitomi_sxs_20180212.tar.gz>`_ and make sure that
your CALDB and CALDB_CONFIG environment variables point to the path where you installed the CALDB files.
See the `CALDB install page <https://heasarc.gsfc.nasa.gov/docs/heasarc/caldb/caldb_install.html>`_ for more information.

Install SPEX through Anaconda
'''''''''''''''''''''''''''''

If you do not have conda yet, please install it using `these instructions <https://docs.conda.io/en/latest/miniconda.html>`_.

Once your conda installation is set up, you can create a spex environment::

    (base) user@unix:~> conda create -n spex python=3.9 numpy scipy astropy pytest jupyter-lab matplotlib pip
    (base) user@unix:~> conda activate spex

Now that we have a spex conda environment, you can install SPEX through conda::

    (spex) user@unix:~> conda install -c spexxray spex pyspextools



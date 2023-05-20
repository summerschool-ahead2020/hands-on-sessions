 .. _sect:software_install:

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
    (base) idies@aaaa:~$ conda create -n spex python=3.9 astropy matplotlib ipykernel mkl=2021.4
    (base) idies@aaaa:~$ conda activate spex
    (spex) idies@aaaa:~$ conda install -c spexxray spex pyspextools
    (spex) idies@aaaa:~$ python -m ipykernel install --user --name spex --display-name "(spex)"

It may be necessary to restart the Jupyter session on Sciserver to load the new SPEX environment into Jupyter properly.
To do that, execute the following steps:

- Close the Jupyter window and go back to the page on Sciserver with the list of your images.
- On this page, you can stop running the image by clicking the red square after the image name. Wait until the image is stopped.
- When the image is fully stopped and the page reloaded, you can click the green triangle to start the image again.
- Click on the name of the image to start Jupyter again. In this new session, SPEX should work in Jupyter.

Running a notebook with SPEX
''''''''''''''''''''''''''''

To run a notebook with SPEX, please select the (spex) kernel from the drop down menu on the top right.
You need to replace '(heasoft)' with '(spex)'. It may be necessary to restart the image for Jupyter to
correctly start the (spex) environment.

If the (spex) environment is not properly loaded, SPEX will not be able to start. It can take some trouble
to make sure that the `(spex)` jupyter kernel also activates the `spex` conda environment. This should be
done automatically, but for some reason it sometimes runs in the `heasoft` environment anyway.

We made the following modifications before successfully running it:

- We have added the line `"conda", "run", "--no-capture-output", "-n", "spex",` to this file
  `~/.local/share/jupyter/kernels/spex/kernel.json` to try to make sure that conda starts the
  spex conda environment::

    {
     "argv": [
      "conda", "run", "--no-capture-output", "-n", "spex",
      "/home/idies/miniconda3/envs/spex/bin/python",
      "-m",
      "ipykernel_launcher",
      "-f",
      "{connection_file}"
     ],
     "display_name": "(spex)",
     "language": "python",
     "metadata": {
      "debugger": true
     }
    }

- We also installed `nb_conda_kernels` into the (heasoft) conda environment: `conda install nb_conda_kernels`.

Restarting the HEASOFT image on Sciserver is necessary to get the (spex) environment to work properly.

Alternative: Renkulab
---------------------

We also have a `Jupyterlab environment with SPEX at Renkulab.io <https://renkulab.io/projects/j.de.plaa/ahead2020-school-spex/sessions/new?autostart=1>`_.
Unfortuntately, HEASOFT is not (yet) working well in Jupyter Lab on Renkulab. The XRISM hands-on session is best done on Sciserver.

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

    (base) user@unix:~> conda create -n spex python=3.9 numpy scipy astropy pytest jupyter-lab matplotlib pip mkl=2021.4
    (base) user@unix:~> conda activate spex

Now that we have a spex conda environment, you can install SPEX through conda::

    (spex) user@unix:~> conda install -c spexxray spex pyspextools

And create a ipykernel for the (spex) environment to work in Jupyter::

    (spex) user@unix:~> python -m ipykernel install --user --name spex --display-name "(spex)"

Troubleshooting
---------------

Importing SPEX in Jupyter fails
'''''''''''''''''''''''''''''''

When you have Jupyter installed in multiple places, it sometimes happens that the wrong Jupyter executable is called. 
If you have trouble importing SPEX, then try to run Jupyterlab like this to force it to use Jupyter from the SPEX 
environment::

    (spex) user@unix:~> $CONDA_PREFIX/bin/jupyter-lab &

See also `this discussion <https://github.com/spex-xray/spex-help/issues/32>`_ for more hints.

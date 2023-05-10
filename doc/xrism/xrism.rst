XRISM hands-on
==============

Analysis of the Hitomi Perseus data
-----------------------------------

The XRISM analysis software is not yet public at the time of the school. However,
the Perseus observations of Hitomi and the Hitomi software are accessible to
everyone. They provide a good example of what a typical data analysis thread
with XRISM will look like.

In this hands-on session, we will analyse a Perseus observation performed by Hitomi
from the original observation files using HEASOFT. We will perform the following
steps:

    - Filter the data (good time intervals and grades),
    - Extract images,
    - Extract lightcurves,
    - Generate expected background spectra,
    - Extract spectra,
    - Generate responses and effective area files,
    - Fit the spectrum.

This analysis involves quite a number of long commands, therefore we provide the
analysis to you in the form of a Jupyter notebook. The goal of this session is
to run the analysis step-by-step and be able to make changes to it if necessary.

Running the notebook on Sciserver
---------------------------------

Make sure that you have setup the Sciserver environment like described in
:ref:`sect:software_install`. Once you have the Jupyter-lab running on
your HEASOFT image on Sciserver, make sure that you start a new terminal
with the (spex) terminal environment.

Once you have successfully entered the (spex) environment, you can go to your
own storage space in the Jupyterlab terminal (replace ``<user>`` by your user name)::

    (spex) idies@aaaa:~$ cd ~/workspace/Storage/<user>/persistent

You can download the notebook and support files into your directory using this git command::

    (spex) idies@aaaa:~/workspace/Storage/<user>/persistent$ git clone https://github.com/summerschool-ahead2020/xrism-hands-on.git

Then make the links to the Hitomi data and background files::

    (spex) idies@aaaa:~/workspace/Storage/<user>/persistent$ cd xrism-hands-on
    (spex) idies@aaaa:~/workspace/Storage/<user>/persistent/xrism-hands-on$ ln -s /FTP/hitomi/data/obs/1/100040030 100040030
    (spex) idies@aaaa:~/workspace/Storage/<user>/persistent/xrism-hands-on$ ln -s /FTP/hitomi/data/nxb_20170510 NXB

And unzip the raytrace fits file in the ``products_sxs`` directory::

    (spex) idies@aaaa:~/workspace/Storage/<user>/persistent/xrism-hands-on$ cd products_sxs
    (spex) idies@aaaa:~/workspace/Storage/<user>/persistent/xrism-hands-on/products_sxs$ gunzip raytrace_ah100040030sxs_p0px1010_ptsrc.fits.gz


Running the notebook on your laptop
-----------------------------------

Make sure that you have setup your laptop environment like described in
:ref:`sect:software_install`. Once you have the Jupyter-lab running in the
(spex) conda environment, you can start a terminal and download the notebook
with support files::

    (spex) user@unix:~$ git clone https://github.com/summerschool-ahead2020/xrism-hands-on.git
    (spex) user@unix:~$ cd xrism-hands-on

Next, we unzip the raytrace file and download the other needed files::

    (spex) user@unix:~/xrism-hands-on$ cd products_sxs
    (spex) user@unix:~/xrism-hands-on/products_sxs$ gunzip raytrace_ah100040030sxs_p0px1010_ptsrc.fits.gz
    (spex) user@unix:~/xrism-hands-on/products_sxs$ cd ..
    (spex) user@unix:~/xrism-hands-on$ 

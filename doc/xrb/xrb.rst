X-ray binaries hands-on session
===================================

You can download the exercises in a directory on your laptop/Sciserver/Renkulab/etc from Github::

  user@linux:~> git clone https://github.com/summerschool-ahead2020/xraybinary-hands-on.git

Thursday, 12:30-13:30, Maria Diaz Trigo

This session is meant to fit high spectral resolution data from a known X-ray binary using continuum and a photoionized plasma model. 

Exercise 1: Chandra/HETG spectra of a black hole X-ray binary
-------------------------------------------------------------

The files below contain a HETG spectrum of the black hole X-ray binary 4U 1630-47. Load the spectra into SPEX and try to fit them with a continuum model. The spectrum is expected to contain absorption lines from a photoionised plasma and perhaps also a broad iron line arising from reflection or scattering in the plasma. Use Gaussians to fit the line features you find. How many lines do you find? Are they in absorption or emission? Would you describe them as “narrow” or “broad”? Can you identify the ions originating the lines? 

•	xrbhetg.res

•	xrbhetg.spo

Hints: The HETG has a High Energy and a Medium Energy grating. Therefore, you will fit two spectra simultaneously in spex. Once you have the model for the first spectrum, you can use ``s.sector_copy(1)`` to create a copy of the model of the first spectrum to fit also to the second spectrum.

From Gatuzz et al. 2019 the continuum spectrum is best fitted with a model made up of a disk blackbody absorbed in the ISM. 

Commands
''''''''
::
    
    s.data("xrbhetg.res","xrbhetg.spo")
    s.dist(1,8.,'kpc') 
    s.ignore(1,1,0.,1.5,'kev')
    s.ignore(1,2,0.,1.5,'kev')
    s.ignore(1,1,10,20,'kev')
    s.ignore(1,2,4.5,20,'kev')
    s.plot_data()
    s.com('hot')
    s.com('dbb')
    s.com_rel(1,2,numpy.array([1])
    s.par(1,1,'nh',8e-2)
    s.par(1,2,'t',2.8)
    s.par(1,2,'norm',1e-9)
    s.sector_copy(1)
    s.par_couple(2,1,'nh',1,1,'nh',1.0)
    s.par_couple(2,2,'t',1,2,'t')
    s.par_couple(2,2,'norm',1,2,'norm',1.0)


Exercise 2: Use self-consistent models
--------------------------------------

The lines fitted in Exercise 1 can also be modelled with self-consistent models such as reflection or a photoionised plasma. Try now to substitute the lines by self-consistent models. First try to include a model for the PIE plasma that accounts for the absorption lines. Do you observe any changes in the continuum? Why do you think this is happening? How many lines do you see in the plasma? Is the plasma representative of an atmosphere or of a wind? Can one slab account for all the absorption? If not, add a second plasma. 

Hint: You can use a distance of 8 kpc. The PIE plasma can be modelled with xabs, which represents absorption by a single slab of photoionized plasma. First fix the turbulent velocity (v) and velocity shift (zv) of the plasma and try to fit the NH and ionization parameter. Once you have a good fit try to improve it by fitting also the velocity width and shift.


Exercise 3: XRISM simulation of an X-ray binary
-----------------------------------------------

At least one of the lines in the spectra fitted in Exercises 1 and 2 is blended due to the resolution of the spectra. The upcoming X-ray microcalorimeter onboard XRISM will allow to resolve the lines and remove degeneracies in spectral fitting. xrbXRISM.spo and xrbXRISM.res contain a simulated XRB spectrum as expected to be observed by XRISM. Repeat the fitting steps from Exercises 1 and 2. Which differences do you observe in the spectral parameters compared to the previous spectra? Which lines are you resolving now compared to previous exercises?


•	xrbXRISM.res

•	xrbXRISM.spo

ISM hands-on
============

You can download the exercises into your Sciserver image or in a directory on your laptop from Github::

  user@linux:~> git clone https://github.com/summerschool-ahead2020/ism-hands-on.git
  
In the `Renkulab image <https://renkulab.io/projects/j.de.plaa/ahead2020-school-spex/sessions>`_, the files 
should already be there in the ``notebooks/ism-hands-on/`` directory.
  
Gas fit exercise
----------------

This folders contains XMM RGS data of the X-ray binary 4U 1820-30. We will use it to fit different gas components along the line of sight.
The filenames are ``simxmm2.res`` and ``simxmm2.spo``.

Fit several components of the ISM with different temperatures. For more inspiration check Costantini et al. 2012 or Rogantini et al. 2021

Use the following settings to start::

    s.dist(1,7.6,'kpc')
    s.com('bb)
    s.com('comt')
    s.com('hot') 
    s.com('amol')
    s.com('hot') 
    s.com('hot') 

relate the models!::

    s.par(1,1,'t',0.14)
    s.par(1,1,'norm',5e-5)
    s.par(1,2,'norm',2.0)
    s.par(1,2,'t0',0.32) 
    s.par(1,2,'t1',29)
    s.par(1,2,'tau',3) 

These are useful dust models for amol::

    s.par(1,4,'i1',3302)
    s.par(1,4,'i2',4103)


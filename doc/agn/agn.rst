AGN hands-on session
====================

The files for this session are available on Github again. You can
download them through the terminal with the command::

   user@linux:~> git clone https://github.com/summerschool-ahead2020/agn-hands-on.git

If you are on Sciserver, it is best to change to your personal storage
folder first. The files are already available on Renkulab in the ``notebooks`` folder.

For the exercises below, load SPEX in your notebook in the usual way. It
is best to have one notebook per exercise::

   from pyspex.spex import Session
   s=Session()

Exercise 1
----------

Files: rgs_warm_absorber.spo combined_simu_rgs.res::

   s.data("combined_simu_rgs.res","rgs_warm_absorber.spo")

We have RGS data of an AGN located at z=0.017 (``s.com('reds')``). Don’t
forget to set the distance: ``s.dist(1,0.017,'z')``.

The continuum is a simple powerlaw (``s.com('pow')``) with a slope
(Gamma) of 2.1. The continuum is absorbed by the cold gas in the Milky
Way (``s.com('hot')``). The temperature for this gas is 1e-6 keV and its
column density is 1.45e20 cm^-2 (1.45e-4 in SPEX units).

At the restframe of the source there are 3 warm absorber components
(``s.com('xabs')``) with log xi=0.51, 1.34, 2.03. The outflow velocity
of the xabs component should be left free (``s.par_free(1,4,'zv')``).

The RGS range goes from 7-35 Ang (=0.35-1.7 keV), so you have to ignore
the energies outside this range::

   s.ignore(1,1,1.E-4,7.0,'ang')
   s.ignore(1,1,35.0,1.E+4,'ang')

Once you have listed all your components,::

   s.com('reds')
   s.com('pow')
   s.com('hot')
   s.com('xabs')
   s.com('xabs')
   s.com('xabs')

don’t forget to relate them. The continuum and every additive
(=emission) component have to be absorbed by the absorbing agents. pow
xabs,xabs,xabs,red,hot Which translates in the SPEX syntax::

   s.com_rel(1,2,numpy.array([4,5,6,1,3]))

NB: xabs is intrinsic to the source (therefore goes to the LEFT of the
redshift), while hot is local to our Galaxy (z=0), therefore goes to the
RIGHT of the redshift.

Now try to fit and plot the data::

   s.plot_data(wave=True)

What are the best fit values for the outflows?

Exercise 2
----------

Files: xrism_agn_simple.spo sxs_nn.res::

   s.data("sxs_nn.res","xrism_agn_simple1.spo")

XRISM-Resolve data go from 0.5 to 12 keV. We should ignore energies
below and above this range::

   s.ignore(1,1,1E-4,0.5,'kev')
   s.ignore(1,1,12.,1E+4,'kev')

Also bin your data for clarity::

   s.bin(1,1,0.5,12,3,'kev')

We have an AGN at z=0.01 observed by XRISM. Don’t forget to set the
distance!::

   s.dist(1,0.01,'z') 

The primary spectrum is a powerlaw (pow) with reflection (refl) with a
high energy cut off at 300 keV. The spectrum is absorbed by one
ultrafast outflow (xabs) and of course from absorption in our Galaxy
(NH=1.45e20, t=1e-6keV)::

   s.com('reds')
   s.com('pow')
   s.com('refl')
   s.com('xabs')
   s.com('hot')
   s.com_rel(1,2,np.array([4,1,5]))
   s.com_rel(1,3,np.array([4,1,5])) 

(remember that xabs is intrinsic to the AGN, while hot is not (see
exercise 1)

NB: some reflection parameters should be linked to the primary powerlaw::

   s.par_couple(1,3,'norm',1,2,'norm',1.)
   s.par_couple(1,3,'gamm',1,2,'gamm',1.)

The parameters for the reflection components are::

   s.par(1,3,'scal',0.5)
   s.par(1,3,'ecut',300)
   s.par(1,3,'pow',0)
   s.par(1,3,'disk',0)
   s.par(1,3,'fgr',0)

All other values can be kept at the default values.

When you reached the best fit check out what are the absorption lines
that you see with the command::

   tral = s.ascdump(1,4,'tral')
   tral.table.show_in_notebook() 

You can check what lines have the larger EW

Exercise 3
----------

Files: xrism_agn_complex sxs_nn.res::

   s.data("sxs_nn.res","xrism_agn_complex1.spo")

XRISM-Resolve data go from 0.5 to 12 keV. We should ignore energies
below and above this range::

   s.ignore(1,1,1.E-4,0.5,'kev')
   s.ignore(1,1,12.,1E+4,'kev')

Also bin your data for clarity::

   s.bin(1,1,0.5,12.,3,'kev')

We have an AGN at z=0.01 observed by XRISM. Don’t forget to set the
distance!::

   s.dist(1,0.01,'z')  

The primary spectrum is a powerlaw (pow) with reflection (refl).

The spectrum is absorbed by absorption in our Galaxy (NH=1.45e20 cm^-2,
t=1e-6) and the same UFO as the previous exercise. However there are now
2 more absorption (xabs) components that you are free to find out.


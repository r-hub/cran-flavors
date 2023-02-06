This became the default in R-devel on May 7, so packages which were not updated 
became uninstallable there.

This area is no longer updated regularly.
---------------------------------------------------------------------

Use of BLAS/LAPACK from C/C++ code
==================================

Installation logs for packages with calls to BLAS or LAPACK routines from
C/C++ code (and include header R_ext/BLAS.h or R_ext/Lapack.h).

The NEWS for R 4.2.0 says

    • USE_FC_LEN_T will become the default: this uses the correct
      prototypes for Fortran BLAS/LAPACK routines called from C/C++,
      and requires adjustment of most such calls - see ‘Writing R
      Extensions’ §6.6.2.  (This has been supported since R 3.6.2.)

and when it did packages here  fail to install.

The checks using pre-4.2.0 were done with

DEFS=-DUSE_FC_LEN_T

in config.site.  Other details follow
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc

Those done since May 7 were done using R-devel with no changes.

For how to adapt your code, see

https://cran.r-project.org/doc/manuals/r-devel/R-exts.html#Fortran-character-strings

Usually all that is needed is to add an appropriate number of
FCONE (no commas) at the end of the call.

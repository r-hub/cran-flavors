Compilation logs for CRAN packages using x86_64 Fedora 34 Linux 
built with configure --enable-lto=R and config.site:

CFLAGS="-g -O2 -Wall -pedantic -mtune=native"
FFLAGS="-g -O2 -mtune=native -Wall -pedantic"
CXXFLAGS="-g -O2 -Wall -pedantic -mtune=native -Wno-ignored-attributes -Wno-deprecated-declarations -Wno-parentheses"
AR=gcc-ar
RANLIB=gcc-ranlib
LTO=-flto=10
LTO_OPT=-flto

and packages under test installed with INSTALL --use-LTO. Other details as
at https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc .

Look for [-Wlto-type-mismatch] warnings.

Where mismatches involve C prototypes for Fortran code, do re-read the
discussion in 'Writing R Extensions' and check using
gfortran -fc--prototypes-external as described there.

Note the difficulties in passing Fortran LOGICAL to or from C discussed at
https://cran.r-project.org/doc/manuals/r-devel/R-exts.html#Fortran-LOGICAL

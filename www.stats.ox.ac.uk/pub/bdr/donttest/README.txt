Tests on x86_64 Linux with R-devel using _R_CHECK_DONTTEST_EXAMPLES_=true

Other details as 
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc 

The latest results are with Fedora 38; earlier ones with F34.

Examples are selected by manual inspection so this may not be fully updated.

Also using _R_CHECK_THINGS_IN_OTHER_DIRS_=true with an exclusion file:
 see the 'R Internals' manual.

2022-01: using

setenv _R_CHECK_LENGTH_1_CONDITION_ abort,verbose
setenv _R_CHECK_LENGTH_1_LOGIC2_ abort,verbose

2022-05: those are now the defaults, but will show in earlier reports.

As fedora-gcc,

https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc

but without the DEFS line and so using C99 inlining semantics.

We know
Evacluster and plotmm are from EMCluster
fedmatch appears to be from stringdist
grainscape and multilaterals are from igraph

Subdirectory 'docker' contains the script for a docker container that has been
used on an x86_64 machine to reproduce most of these. (On Linux but docker
in prinicple also works on Windows and Intel or Apple Silicon macOS.)
See its comments for how to use it.

Beware that if you have customizations in e.g. ~/.R/Makeconf these may
well negate the ability to reproduce the segfaults.


Alternatively
-------------

Many of the issues are from passing as.double(NULL) or as.integer(NULL)
to .C or .Fortran where the compiled code expects to be pased a vector
of lemgth at least one.

[Support for this experimental check has been removed.]
If R-devel is compiled with 

-DR_LESS_COERCION_FROM_NULL

(for exaxmple by setting DEFS in config.site to this), then these become 
errors and the traceback on error will almost always pinpoint the 
(first) issue.  Logs from this approach are in subdirectory Alternative.
(Such calls could perhaps be legitimate, but most are a problem.)


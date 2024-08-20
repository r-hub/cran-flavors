Tests with STRICT_R_HEADERS defined to 1. This removes

- the legacy definition of PI (use POSIX's M_PI, available in R 'for ever').
- the RS.h declarations for Calloc, Realloc, Free (use R_ forms
  available since R 3.4.0).

The aim is to clean the namespace: in particular having a definition
for Free has conflicted with some packages' C++ code.

Otherwise as for the fedora-gcc checks:
see https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc

It is planned that this will become the default for R 4.5.0.

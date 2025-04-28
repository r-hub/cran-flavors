Installation checks with a snapshot of GCC pre-15.
This defaults the C compiler to -std=gnu23.
The current description of changes is

https://gcc.gnu.org/gcc-15/changes.html

See also

https://gcc.gnu.org/gcc-15/porting_to.html

Also (a late change) header omp.h defines 'omp' as a C++ namespace and so
if cannot tbe used as an identifier, e.g. a function name.

Other details as https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc

Debian unstable and Ubuntu have a package 'gcc-snapshot'.

GCC 15 was released on 2025-04-25

This area is no longer update as the mainstream checks will or have move to
GCC 15.1.

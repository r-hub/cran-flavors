Tests using R-devel on x86_64 Fedora 44 Linux with alternative BLAS/LAPACK
implementations.  Except as noted below, R was configured as per
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc

ATLAS:
(<https://en.wikipedia.org/wiki/Automatically_Tuned_Linear_Algebra_Software>,
last release  2016-07)
Serial ATLAS using the Fedora shared libraries. (Currently version 3.10.3.)
libRblas.so was replaced by a symlink to /usr/lib64/atlas/libsatlas.so .
It reports using LAPACK 3.12.0.

Becasue this is precomppild by Fedora, it is NOT tuned to the platform in use.

2026-09-01: no longer run regularly.

BLIS:
(<https://en.wikipedia.org/wiki/BLIS_(software)>)
Serial BLIS using the Fedora shared libraries. (Currently version 2.0-5)
libRblas.so was replaced by a symlink to /usr/lib64/libblis.so.4
It reports using the system LAPACK 3.12.0.

MKL:
(<https://en.wikipedia.org/wiki/Math_Kernel_Library>)
Serial Intel MKL 2026.1.0, which reports LAPACK 3.12.1.

Older checks (before 2026-07) used Intel MKL '2023.2.0',
used to build Rblas and also provided LAPACK version 3.10.1.

R was configured by (csh script)

setenv MKL_LIB_PATH /usr/local/MKL/mkl/lib/intel64
setenv LD_LIBRARY_PATH $MKL_LIB_PATH
setenv MKL "-L$MKL_LIB_PATH -lmkl_gf_lp64 -lmkl_core -lmkl_sequential"
~/R/svn/R-devel/configure -C --with-blas="$MKL" --with-lapack --enable-lto=R

OpenBLAS:
(<https://en.wikipedia.org/wiki/OpenBLAS>)
Serial OpenBLAS using the Fedora shared libraries (currently version 0.3.29).
libRblas.so was replaced by a symlink to /usr/lib64/libopenblas.so (part of
openblas-devel, linked from openblas-serial). This reports using LAPACK 3.12.0.


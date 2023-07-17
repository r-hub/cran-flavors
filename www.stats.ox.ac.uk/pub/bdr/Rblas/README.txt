Tests using R-devel on x86_64 Fedora 34 Linux with alternative BLAS/LAPACK
implementations.  Except as noted below, R was configured as per
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc

ATLAS:
Serial ATLAS using the Fedora shared libraries. (Currently version 3.10.3.)
libRblas.so was replaced by a symlink to /usr/lib64/atlas/libsatlas.so .
It reports using LAPACK 3.10.0.

MKL:
Intel MKL '2023.1.0' used to build Rblas and also provides LAPACK
(which is version 3.10.1).  R was configured by (csh script)

setenv MKL_LIB_PATH /usr/local/MKL/mkl/lib/intel64
setenv LD_LIBRARY_PATH $MKL_LIB_PATH
setenv MKL "-L$MKL_LIB_PATH -lmkl_gf_lp64 -lmkl_core -lmkl_sequential"
~/R/svn/R-devel/configure -C --with-blas="$MKL" --with-lapack --enable-lto=R

OpenBLAS:

Serial OpenBLAS using the Fedora shared libraries (currently version 0.3.19).
libRblas.so was replaced by a symlink to /usr/lib64/libopenblas.so (part of
openblas-devel, linked from openblas-serial). This reports using LAPACK 3.9.0.

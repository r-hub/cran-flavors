Checks of packages with C/C++/Fortran compiled code, using the
Intel compilers icx/ipcx/ifx from oneAPI 2024.2.1 and oneMKL 2023.2.0,
with settings as described in 
https://cran.r-project.org/doc/manuals/r-devel/R-admin.html#Intel-compilers

The C stack limit had to be increased to 50M

For C++ this uses the system libstdc++ headers andlibrary, in this case
those  provided by GCC 12 (and not the GCC 14 versions used for the fedora-gcc
checks).  This causes some warnings like

  /usr/lib/gcc/x86_64-redhat-linux/12/../../../../include/c++/12/bits/stl_tempbuf.h:263:8: warning: 'get_temporary_buffer<arma::arma_sort_index_packet<double>>' is deprecated [-Wdeprecated-declarations]

and those have been moved to sub-directory Old.

The 2024.2.0 version of ifx had hardcoded liinks to the 2024.1.0 version of the 
C libraries, so a ln -s 2024.2.0 2024.1.0 in the 'oneapi/compiler' 
directory was needed.


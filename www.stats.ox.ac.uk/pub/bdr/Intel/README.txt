Checks of packages with C/C++/Fortran compiled code, using the
Intel compilers icx/ipcx/ifx from oneAPI 2024.2.0 and oneMKL 2023.2.0,
with settings as described in 
https://cran.r-project.org/doc/manuals/r-devel/R-admin.html#Intel-compilers

The C stack limit had to be increased to 50M

For C++ this uses the system libstdc++ library, in this case that provided by
GCC 12 (and not the GCC 14 versions used for the fedora-gcc checks).

The 2024.2.0 version of ifx has hardcoded liks to the 2024.1.0 version of the 
C libraries, so a ln -s 2024.2.0 2024.1.0 in the 'oneapi/compiler' 
directory was needed.


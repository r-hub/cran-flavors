Checks of packaes with C/C++/Fortran compiled code, using the
Intel compilers icx/ipcx/ifx from oneAPI 2024.0 and oneMKL 2023.2.0,
with settings as described in 
https://cran.r-project.org/doc/manuals/r-devel/R-admin.html#Intel-compilers

The C stack limit had to be increased to 50M

One quirk is that ifx treats files with extension .f90 as free-format,
but not those with extension .f95. This has been worked around for packages
without a src/Makefile -- see the R-admin manual.


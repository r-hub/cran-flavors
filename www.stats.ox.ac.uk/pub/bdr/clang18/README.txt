AS LLVM 18 is used for the main fedora-clang results, this only
reports historical issues.

Tests as for the main fedora-clang checks but using LLVM pre-18
including its flang-new as the Fortran compiler.
Other details as for 
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-clang .

flang-new no longer accepts the GNU flag -pipe.

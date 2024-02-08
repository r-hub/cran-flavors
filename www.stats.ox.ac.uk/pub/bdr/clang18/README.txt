Once LLVM 18 is use for the main fedora-clang results, this will only
report historical issues.

Tests as for the main fedora-clang checks but using LLVM pre-18
including its flang-new as the Fortran compiler.
Other details as for 
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-clang .

flang-new no longer accepts the GNU flag -pipe.

LLVM 18 is currently scheduled for release in 'early' March 2024.
LLVM has changed its numbering scheme to be closer to GCC, so the
releases will be 18.1.x.


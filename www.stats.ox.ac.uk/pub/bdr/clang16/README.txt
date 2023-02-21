As for fedora-clang, but NOT using
 -Wno-error=enum-constexpr-conversion -D_HAS_AUTO_PTR_ETC=0

Other details as
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-clang

References for Rf_length in system headers come from includeing R headers
before system headers rather than after: see 'Writing R Extnesions'.

std:unary_function was deprecated in C+11 and removed in C++17, and finally
in clang 16 in C++17 mode.  Boost 1.81 is still using it.


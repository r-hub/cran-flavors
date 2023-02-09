Tests as for fedora-clang but using clang 16.0.0rc2 rather than 15.0.7.
This is scheduled for release on Mar 7th.

Currently using C23 as the default C standard (but C23 issues are
reported elsewhare).

Other details as
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-clang

References for Rf_length in system headers come from includeing R headers
before system headers rather than after: see 'Writing R Extnesions'.

The [-Wenum-constexpr-conversion] errors seen in

RSQLite

are from the old Boost headers.

std:unary_function was deprecated in C+11 and removed in C++17, and finally
in clang 16 in C++17 mode.  Boost 1.81 was still using it.


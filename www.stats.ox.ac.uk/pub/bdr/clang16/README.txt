clang 16.0.0 is now used for the main fedora-clang checks, so this is
largely historical -- it also highlights some warnings only in clang >= 16.

References to Rf_length in system headers come from includeing R headers
before system headers rather than after: see 'Writing R Extnesions'.

std:unary_function was deprecated in C+11 and removed in C++17, and finally
in clang 16 in C++17 mode.  Boost 1.81 is still using it (in 2023!).
This and more can be worked around by including -D_HAS_AUTO_PTR_ETC=0
in PKG_CPPFLAGS or defiining it in headers/code files using Boost headers.

Tests of memory access errors, on x86_64 Linux
==============================================

(Currently using Fedora 36 except valgrind under Fedoora 38.)

There is a directory for each package with a 00check.log file documenting the
package version and the version of R used.  For {gcc,clang}-ASAN this may
also report errors, including from examples.

How to run and interpret these (with links to further information) is in §4.3 of 'Writing R Extensions'.  The settings used are listed by sub-directory in the rest of this file.

Results for archived packages will likely have been made with earilier 
versions of the compilers.


clang-ASAN
Using clang 19 built with libc++/libc++abi as the default C++ library,
and flang-new 19 as the Fortran compiler. Note that the latter does
not yet support sanitizers.
[For a version built to default to libstdc++ (as shipped by Debian/Ubuntu),
add -stdlib=libc++ to the CXX line and install the libc++-dev package.]

config.site:
CC="clang -fsanitize=addres-fno-omit-frame-pointer"
CXX="clang++ -fsanitize=address,undefined -fno-omit-frame-pointer -frtti"
CFLAGS="-g -O3 -Wall -pedantic"
CXXFLAGS="-g -O3 -Wall -pedantiic"
FC=flang-new
FFLAGS="-O2 -pedantic"
SHLIB_OPENMP_FFLAGS=

and environment variables
setenv ASAN_OPTIONS detect_leaks=0
setenv RJAVA_JVM_STACK_WORKAROUND 0
setenv RGL_USE_NULL true
(alloc-dealloc mismatches were seen in system libraries used by rgl)
setenv R_DONT_USE_TK true
(There were ASAN errors in X libraries called from Tk initialization.)

[Results prior to 2024-02-17 were made with clang 16 and gfortran 13.2.]
[2024-12-19
## fortify is said to be broken with sanitizers: https://discourse.llvm.org/t/asan-fortify-source/81056
so is no longer used.]
[2024-12-23: selected revdeps are installed with ASAN, so results reflect
buffere overflows etc in those revdeps.]

clang-UBSAN:
Using clang 19 built with libc++/libc++abi as the default C++ library,
and flang-new 19 as the Fortran compiler. Note that the latter does
not yet support sanitizers.
[For a version built to default to libstdc++ (as shipped by Debian/Ubuntu),
add -stdlib=libc++ to the CXX line and install the libc++-dev package.]

An unaltered build of R was used, but each package was tested with 
R_MAKEVARS_USER pointing to a file containing

CC=/usr/local/clang19/bin/clang -fsanitize=undefined -fno-sanitize=function -fno-omit-frame-pointer
CXX=/usr/local/clang19/bin/clang++ -fsanitize=undefined -fno-sanitize=function -fno-omit-frame-pointer -frtti
UBSAN_DIR = /usr/local/clang19/lib/clang/19/lib/x86_64-unknown-linux-gnu
SAN_LIBS = -L$(UBSAN_DIR) -Wl,-rpath,$(UBSAN_DIR) -lclang_rt.ubsan_standalone

as discussed in 'Writing R Extensions'.

[Results prior to 2024-02-17 were made with clang 16 and gfortran 13.2.]



gcc-ASAN, gcc-UBSAN:
gcc 14.2 with config.site:
CC="gcc-14 -fsanitize=address,undefined,bounds-strict -fno-omit-frame-pointer"
CXX="g++-14 -fsanitize=address,undefined,bounds-strict -fno-omit-frame-pointer"
CFLAGS="-g -O2 -Wall -pedantic -mtune=native -fsanitize=address -Wno-stringop-truncation -Wno-alloc-size-larger-than"
FC=gfortran-14
FFLAGS="-g -O2 -mtune=native"
CXXFLAGS="-g -O2 -Wall -pedantic -mtune=native -Wno-ignored-attributes -Wno-deprecated-declarations -Wno-stringop-truncation -Wno-alloc-size-larger-than"
MAIN_LDFLAGS="-fsanitize=address,undefined -pthread"

[2024-12-05: now bulding R with --enable-lto=R, hence adding

AR=gcc-ar
RANLIB=gcc-ranlib
LTO=-flto=10
LTO_OPT=-flto

]

Added -Wno-stringop-truncation following
https://gcc.gnu.org/bugzilla/show_bug.cgi?id=108939
Dropped -Wp,-D_FORTIFY_SOURCE=3 : see the comment under clang-ASAN.

~/.R/Makevars:
CC = gcc-14 -std=gnu99 -fsanitize=address,undefined,bounds-strict -fno-omit-frame-pointer
FC = gfortran-14 -fsanitize=address

and environment variables
setenv ASAN_OPTIONS 'detect_leaks=0'
[RcppParallel is run adding detect_odr_violation=0]
setenv UBSAN_OPTIONS 'print_stacktrace=1'
setenv RJAVA_JVM_STACK_WORKAROUND 0
setenv RGL_USE_NULL true
setenv R_DONT_USE_TK true


valgrind:
Running R CMD check --use-valgrind with an instrumented (level 2) build of R,
currently using valgrind 3.24.0 on Fedora 40.

configured by:
.../configure -C --with-valgrind-instrumentation=2

with config.site:

CFLAGS="-g -O2 -Wall -pedantic -mtune=native"
CXXFLAGS="-g -O2 -Wall -pedantic -mtune=native"
FFLAGS="-g -O2 -mtune=native"
FCFLAGS="-g -O2 -mtune=native"

and environment variables

setenv RJAVA_JVM_STACK_WORKAROUND 0
setenv R_DONT_USE_TK true

The following valgrind suppression file is used:

{
   Suppression for wcsrtombs
   Memcheck:Cond
   fun:__wcsnlen_sse4_1
   fun:wcsrtombs
   fun:wcstombs
}

{
   Suppression for do_makename
   Memcheck:Addr16
   fun:__wcsnlen_sse4_1
   fun:wcsrtombs
   fun:wcstombs
}

NB: there are  SSAN/UBSAN results for macOS at
https://www.stats.ox.ac.uk/pub/bdr/M1-SAN/


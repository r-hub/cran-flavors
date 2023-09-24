Tests of memory access errors, on x86_64 Linux (currently Fedora 36).

There is a directory for each package with a 00check.log file documenting the
package version and the version of R used.  For {gcc,clang}-ASAN this may
also report errors, including from examples.

How to run and interpret these (with links to further information) is in §4.3 of 'Writing R Extensions'.  The settings used are listed by sub-directory in the rest of this file.


clang-ASAN, clang-UBSAN:
Using clang 16 built with libc++/libcxxabi as the default C++ library,
and gfortran 13.2. (Older results with clang 15 or fortran 12.)
[For a version built to default to libstdc++ (as shipped by Debian/Ubuntu),
add -stdlib=libc++ to the CXX line and install the libc++-dev package.]
NB: unlike the fedora-clang resulta this does not yet use clang 17 and 
flang 17, as R does not compile under ASAN for those compilers.

config.site:
CC="clang -fsanitize=address,undefined -fno-sanitize=float-divide-by-zero -fno-sanitize=alignment -fno-omit-frame-pointer"
CXX="clang++ -fsanitize=address,undefined -fno-sanitize=float-divide-by-zero -fno-sanitize=alignment -fno-omit-frame-pointer -frtti"
CFLAGS="-g -O3 -Wall -pedantic"
FFLAGS="-g -O2 -mtune=native"
CXXFLAGS="-g -O3 -Wall -pedantic"
MAIN_LD="clang++ -fsanitize=undefined,address"

and environment variables
setenv ASAN_OPTIONS detect_leaks=0
setenv UBSAN_OPTIONS 'print_stacktrace=1'
setenv RJAVA_JVM_STACK_WORKAROUND 0
setenv RGL_USE_NULL true
(alloc-dealloc mismatches were seen in system libraries used by rgl)
setenv R_DONT_USE_TK true
(There are ASAN errors in X libraries called from Tk initialization.)


gcc-ASAN, gcc-UBSAN:
gcc 13.2 with config.site:
CXX="g++ -fsanitize=address,undefined,bounds-strict -fno-omit-frame-pointer"
CFLAGS="-g -O2 -Wall -pedantic -mtune=native -fsanitize=address"
FFLAGS="-g -O2 -mtune=native"
CXXFLAGS="-g -O2 -Wall -pedantic -mtune=native"
MAIN_LDFLAGS="-fsanitize=address,undefined -pthread"

~/.R/Makevars:
CC = gcc -std=gnu99 -fsanitize=address,undefined -fno-omit-frame-pointer
F77 = gfortran -fsanitize=address
FC = gfortran -fsanitize=address

and environment variables
setenv ASAN_OPTIONS 'detect_leaks=0:detect_odr_violation=0'
[Experimenting without detect_odr_violation=0]
setenv UBSAN_OPTIONS 'print_stacktrace=1'
setenv RJAVA_JVM_STACK_WORKAROUND 0
setenv RGL_USE_NULL true
setenv R_DONT_USE_TK true


valgrind:
Running R CMD check --use-valgrind with an instrumented (level 2) build of R,
currently using valgrind 3.21.0 on Fedora 38.

configured by:
.../configure -C --with-valgrind-instrumentation=2

and formerly --with-system-valgrind-headers

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


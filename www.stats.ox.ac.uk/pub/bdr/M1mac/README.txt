Check results using R-devel on an arm64 ('M1') Mac running macOS 13.2.1
'Ventura' with Xcode/CLT 14.2 and the build of gfortran (a fork of 12.2) from
https://github.com/R-macos/gcc-12-branch/releases/tag/12.2-darwin-r0

Timezone Europe/London
Locale en_GB.UTF-8, LC_COLLATE=C

Details as in the R-admin manual, with config.site containing

CC=clang
OBJC=$CC
FC="/opt/gfortran/bin/gfortran -mtune=native"
CXX=clang++
CFLAGS="-falign-functions=8 -g -O2 -Wall -pedantic -Wconversion -Wno-sign-conversion"
CXXFLAGS="-g -O2 -Wall -pedantic -Wconversion -Wno-sign-conversion"
CPPFLAGS=-I/opt/R/arm64/include
FFLAGS="-g -O2 -mmacosx-version-min=12.0"
FCFLAGS="-g -O2 -mmacosx-version-min=12.0"
LDFLAGS=-L/opt/R/arm64/lib
R_LD_LIBRARY_PATH=/opt/R/arm64/lib

(The F[C]FLAGS have been needed as some compilers will compile for
macOS 13.0 and the linker will warn.)

External libraries were where possible installed via minor
modifications to Simon Urbanek's 'recipes' at
https://github.com/R-macos/recipes .  The exceptions are those which
need to use dynamic libraries (such as openmpi).

Currently this uses PROJ 9.2.0, GEOS 3.11.1, GDAL 3.6.2 and gsl 2.7.1.

pandoc is the Intel Mac version, currently 3.1.1 (and updated often).
(There is a self-contained arm64 build available from Homebrew, 
another of 2.14.2 from https://mac.r-project.org/libs-arm64/.)

Java is 17.0.6 from https://adoptium.net

JAGS is a binary install from 
https://sourceforge.net/projects/mcmc-jags/files/JAGS/4.x/Mac%20OS%20X/

ghoatscript is 10.0.0 built from the sources. (MacTeX 2022 provides 9.55.0).

There is a testing service for the CRAN M1mac setup at
https://mac.r-project.org/macbuilder/submit.html

Some ways in which this may differ from the CRAN checks:

- Using R-devel not R 4.[12].x
- timezone is Europe/London not Pacific/Auckland
- OS and Command Line Tools are kept up-to-date (at present the CRAN
    check service is running macOS 11 and Xcode/CLT 12).
- Later C/C++ compilers, different flags.
- External software is (mainly) kept up-to-date -- see above.
    This includes using Java 17 -- I believe the CRAN checks use a
      patched (by Zulu) Java 11.
    And cmake, currently 3.25.2.
    OpenMPI is installed for Rmpi, bigGP and pbdMPI
- 'R' is not on the path -- checking is by 'Rdev'.
- Package INLA is installed -- requires a binary install on Macs.

Note that Apple has deprecated C functions sprintf and vsprintf in
macOS 13 SDK: this also affect users of C++.  (And the much less
commonly used and widely deprecated gets, mktemp and tmpnam.)

Packages with non-default installs:

RVowpalWabbit: --configure-args='--with-boost=/opt/R/arm64'
rgdal: --configure-args='--with-data-copy --with-proj-data=/opt/R/arm64/share/proj'
sf: --configure-args='--with-data-copy --with-proj-data=/opt/R/arm64/share/proj'

Options used for 'R CMD check':

setenv _R_CHECK_FORCE_SUGGESTS_ FALSE
setenv LC_CTYPE en_GB.UTF-8
setenv RMPI_TYPE OPENMPI
setenv R_BROWSER false
setenv R_PDFVIEWER false
setenv OMP_NUM_THREADS 2
setenv _R_CHECK_INSTALL_DEPENDS_ true
#setenv _R_CHECK_SUGGESTS_ONLY_ true
setenv _R_CHECK_NO_RECOMMENDED_ true
setenv _R_CHECK_TIMINGS_ 10
setenv _R_CHECK_DEPRECATED_DEFUNCT_ true
setenv _R_CHECK_CODE_ASSIGN_TO_GLOBALENV_ true
setenv _R_CHECK_CODE_DATA_INTO_GLOBALENV_ true
setenv _R_CHECK_SCREEN_DEVICE_ warn
setenv _R_CHECK_S3_METHODS_NOT_REGISTERED_ true
setenv _R_CHECK_OVERWRITE_REGISTERED_S3_METHODS_ true
setenv _R_CHECK_NATIVE_ROUTINE_REGISTRATION_ true
setenv _R_CHECK_FF_CALLS_ registration
setenv _R_CHECK_PRAGMAS_ true
setenv _R_CHECK_COMPILATION_FLAGS_ true
setenv _R_CHECK_COMPILATION_FLAGS_KNOWN_ "-Wconversion -Wno-sign-conversion"
setenv _R_CHECK_THINGS_IN_TEMP_DIR_ true
setenv _R_CHECK_THINGS_IN_TEMP_DIR_EXCLUDE_ "^ompi"
setenv _R_CHECK_MATRIX_DATA_ TRUE
setenv _R_CHECK_ORPHANED_ true

setenv OMP_THREAD_LIMIT 2
setenv R_DEFAULT_INTERNET_TIMEOUT 600
setenv NOAWT 1
setenv RGL_USE_NULL true
setenv WNHOME /usr/local/wordnet-3.1

setenv _R_CHECK_XREFS_USE_ALIASES_FROM_CRAN_ TRUE

setenv _R_CHECK_RD_VALIDATE_RD2HTML_ true
setenv _R_CHECK_RD_MATH_RENDERING_ true

and cosmetically

setenv _R_CHECK_VIGNETTES_SKIP_RUN_MAYBE_ true
setenv _R_CHECK_TESTS_NLINES_ 0
setenv _R_CHECK_VIGNETTES_NLINES_ 0

A parellel make is used and packages are checked in parallel --
installing or checking a single package may use up to 8 CPUs.

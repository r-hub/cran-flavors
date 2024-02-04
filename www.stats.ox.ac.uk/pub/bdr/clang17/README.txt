2023-09-20: the fedora-clang checks has switched to LLVM 17.0.1 so 
this area will not be updated.  It still contains check logs for
packages which have been archived before or on that date.

2024-02-03: also used to record (direct) installation and check failures
not seen with fedora-gcc checks.

Tests as for the main fedora-clang checks but using LLVM pre-17
including flang-new as the Fortran compiler.
Other details as for 
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-clang .

The clang and LLVM release notes are at
https://releases.llvm.org/17.0.1/tools/clang/docs/ReleaseNotes.html
https://releases.llvm.org/17.0.1/docs/ReleaseNotes.html

Pre-built compilers may be available at
https://github.com/llvm/llvm-project/releases


References to Rf_length in system headers come from including R headers
before system headers rather than after: see 'Writing R Extnesions'.  For
this toolchain, the problems are seen in files included from the 
C++ header <vector>.

That manual says

"This remapping can cause problems, and can be eliminated by defining
R_NO_REMAP (before including any R headers) and prepending ‘Rf_’ to all
the function names used from Rinternals.h and R_ext/Error.h. These problems
can usually be avoided by including other headers (such as system headers
and those for external software used by the package) before any R headers.
(Headers from other packages may include R headers directly or via inclusion
from further packages, and may define R_NO_REMAP with or without including
Rinternals.h.) "


Notes for the Fortran compiler, 'flang-new':

dlgama is a GNU extension: the F2008 function is LOG_GAMMA.
etime is a GNU extension which can be replaced by CPU_TIME and/or
  SYSTEM_CLOCK, but seems unused by the packages calling it.
getpid is a GNU extension.
isnan is a GNU extension.  There are standard ways to do this as from F2003,
  or you can use if(my_var /= my_var).


Some packages needed the stack limit increased (from 20MB to 50MB):
KFAS NPRED SynchWave TSSS calcWOI sequoia


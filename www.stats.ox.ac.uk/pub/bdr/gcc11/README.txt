Logs from checks of packages using gcc 11.2 (or for archived packages, 11.1 or
pre-releases) compiled from source on Fedora 32.

gcc 11 is the current version and used by e.g. Fedora 34.  The issues 
for current packages were confirmed for gcc trunk ('12.0.0') and 
with Fedora 34 in 2021-07.

Details as https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc

The message

error: 'numeric_limits' is not a member of 'std'

indicates a missing <limits> header

and

'set_terminate' was not declared in this scope;

indicates a missing <exception> header (and maybe better to use std::set_terminate).

Both are included by other headers in earlier versions of g++/libstdc++.


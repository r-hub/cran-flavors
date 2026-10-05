Check logs from cheking CRAN packages on the M1mac system detailed
at https://www.stats.ox.ac.uk/pub/bdr/M1mac/README.txt .

R and packages were compiled with ASAN + UBSAN (see
https://cran.r-project.org/doc/manuals/r-devel/R-exts.html#Checking-memory-access
)

using config.site containing

CC="clang -mmacos-version-min=26 -fsanitize=address,undefined"
CXX="clang++ -mmacos-version-min=26 -fsanitize=address,undefined"
REC_INSTALL_OPT=--dsym

and checked with environment variables

setenv MallocNanoZone 0
setenv UBSAN_OPTIONS 'print_stacktrace=1'


Per-package notes
-----------------

Also Linux: nonmem2rx

Alignment:
 (Those which are 0x000000000001 are likely attempts to access an
  element of a 0-lemgth R vector.  Note that on macOS calling memcpy
  etc with a zero size does access the 'src' pointer.  Some people
  claim (e.g. https://en.cppreference.com/cpp/string/byte/memcpy)
  'src' must be a non-NULL and valid pointer, but the C, C++ and POSIX
  standards do not seem to.)

Archived: CovRegRF LTRCforests RFpredInterval SlaPMEG apLCMS
  bayestransmission mninred spRFA

isopam no longer has compiled code.

(reported)
(and ignored)
pander
(repeatedly) terra 

gtools, restfulr: in system socket headers.

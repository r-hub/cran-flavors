Upadate: 2023-04-26
The main fedora-gcc checks have been migrated to GCC 13,
and this area is only for historical records on archived packages.

Tests as for fedora-gcc but with GCC trunk aka pre-13.0.0 -- the
logs record the snapshot used.

Further details as 

https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc

Reports that types such as uint64_t are undeclared indicate that header
<cstdint> (C++) or <stdint.h> (C) have not been included explicitly --
they are presumably included by some other header on earlier versions of gcc,
or by other compilers or platforms.

See also https://gcc.gnu.org/gcc-13/porting_to.html .

Ttests on x86_64 Linux with R-devel using _R_CHECK_DEPENDS_ONLY_=true,
so packages in Suggests (and Enhances) are not available (other
than recommended packages).

For this to work as intended, add-on packages need to be installed
in a library other than .Library.

Other details as 
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-gcc

Packages get reported here when they have used a suggested/enhances 
package which is unavailable.  Since such packages come and go, they
will continue to be checked and reported here if they fail again.


Tests as for fedora-clang but using

CC='clang -std=gnu2x'

Other details as
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-clang

[The checks were done with clang 16.0.0rc, but should be reproducible
with the current clang 15.0.x.]

Details of the upcoming C23 standard can be found at

https://en.cppreference.com/w/c/23
https://thephd.dev/c23-is-coming-here-is-what-is-on-the-menu
https://open-std.org/JTC1/SC22/WG14/www/docs/n3054.pdf

Note that 'bool', 'false' and 'true' have become reserved words.

Some of this, including the new reserved words, is also seen with gcc pre-13.

Becasue mgcv is currently failing, you may not be able to build R with
this setting of CC -- rather use it in a personal Makevars file when
checking the package
-- https://cran.r-project.org/doc/manuals/r-devel/R-admin.html#Customizing-package-compilation

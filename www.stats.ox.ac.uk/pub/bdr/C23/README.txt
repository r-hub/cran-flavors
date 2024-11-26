Tests as for fedora-clang but using

CC='clang -std=gnu23'

(-std=gnu2x for earlier versions of clang).

Other details as
https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-clang

Details of the upcoming C23 standard can be found at

https://en.cppreference.com/w/c/23
https://thephd.dev/c23-is-coming-here-is-what-is-on-the-menu
https://open-std.org/JTC1/SC22/WG14/www/docs/n3054.pdf

Note that 'bool', 'false' and 'true' have become reserved words.

Some of this, including the new reserved words, is also seen with gcc >= 13.

tth has since had added 

SystemRequirements: USE_C17

to it DESCRIPTION file which ensures compilation with C17.


Checks using LLVM 23.1.0, released 2026-08-25.

Other details as https://www.stats.ox.ac.uk/pub/bdr/Rconfig/r-devel-linux-x86_64-fedora-clang.

The fedora-clang checks differ only in that 
_LIBCPP_KEEP_TRANSITIVE_INCLUDES_LLVM23 
is defined in CXXFLAGS.

Release notes are available at

https://releases.llvm.org/23.1.0/tools/clang/docs/ReleaseNotes.html
https://releases.llvm.org/23.1.0/tools/flang/docs/ReleaseNotes.html
https://releases.llvm.org/23.1.0/projects/libcxx/docs/ReleaseNotes.html

which includes

"libc++ has dropped a lot of transitive includes in all language modes.
This improves compile time significantly, but causes programs which rely
on these includes to not compile anymore. Any errors caused by this
should be fixable by including the correct header. To ease the transition
_LIBCPP_KEEP_TRANSITIVE_INCLUDES_LLVM23 can be defined, which includes
the removed headers again. This macro will be removed in LLVM 24."

So if declaration(s) (especially in std:) are reported as missing, do ensure
that the header(s) which declare them are included.  Most commonly
<algorithm> or <iterator> is missing.  gamstranfer needed <type_traits>

People writing C and calling it C++ need to include headers such as
<cstdlib>, <cstddef>, <cmath> or <ctime>. These have been needed for

    nullptr_t size_t fabs isnan log sqrt clock localtime time

This is about libc++: some people build clang++ to by default link to
GCC's libstdc++, which has a compltely separate set of C++ headers.

LLVM provides some binary builds (those for -rc3 suffice) at
 https://github.com/llvm/llvm-project/releases

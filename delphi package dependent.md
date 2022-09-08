# See:
- [Error F2063 Could not compile used unit (of dependent package)](https://stackoverflow.com/questions/28084508/error-f2063-could-not-compile-used-unit-of-dependent-package)

# 建议：

Delphi IDE is far from perfect when it comes to editing/compiling packages but you should solve the problem on your side - configure your packages better and Delphi will compile them correctly.

I can only give you general advices addressing the info given:

    If you need a common include file for 2 packages create a separate directory for the file and add this directory to the search paths of both packages (in Base build configuration).

    Never keep .dcu's in the same folders with source files; always set "unit output directory" option for your packages (also in Base build configuration); I recommend $(BDSCOMMONDIR)\MyPacks\$(Config)\$(Platform) as such directory for your packages; if you already have .dcu's in the source (.pas) folders delete them, does not matter which Delphi version created these .dcu's.

    Never add paths to dependent package's sources to the search path, only paths to compiled .dcu's (would be $(BDSCOMMONDIR)\MyPacks\$(Config)\$(Platform) if you follow previous advice).



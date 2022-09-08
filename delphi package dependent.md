# See:
- [Error F2063 Could not compile used unit (of dependent package)](https://stackoverflow.com/questions/28084508/error-f2063-could-not-compile-used-unit-of-dependent-package)
- [Delphi package conflicts with itself in a subpackage](https://stackoverflow.com/questions/41101857/delphi-package-conflicts-with-itself-in-a-subpackage)

# 建议一：

Delphi IDE is far from perfect when it comes to editing/compiling packages but you should solve the problem on your side - configure your packages better and Delphi will compile them correctly.

I can only give you general advices addressing the info given:

 If you need a common include file for 2 packages create a separate directory for the file and add this directory to the search paths of both packages (in Base build configuration).

  Never keep .dcu's in the same folders with source files; always set "unit output directory" option for your packages (also in Base build configuration); I recommend ```$(BDSCOMMONDIR)\MyPacks\$(Config)\$(Platform)``` as such directory for your packages; if you already have .dcu's in the source (.pas) folders delete them, does not matter which Delphi version created these .dcu's.

  Never add paths to dependent package's sources to the search path, only paths to compiled .dcu's (would be ```$(BDSCOMMONDIR)\MyPacks\$(Config)\$(Platform)``` if you follow previous advice).
  
  # 建议二：
  
  

There are no "subpackages". Each package is a package on its own. But let's assume you have the following setup:

    package1
        unit1A
        unit1B
        unit1C
    package2
        unit2A uses unit1A
        unit2B uses unitX
    package3
        unit3A uses unit1B
        unit3B uses unitX

If any of unit2A, unit2B, unit3A, or unit3B needs to use a unit from package1, then that package should be in the requires section of package2 or package3, but the units unit1A, unit1B or unit1C should not be in the contains section of these packages, nor should they be silently included — you get a message if that happens.

In the setup above, if unitX is not in a package in the requires section of package1 and package2, it gets silently included. If that happens in more than one package, you have a naming conflict. So you either include it in package2 and require package2 from package3 too, or you put it into a package of its own.

So whatever you do:

- Each unit (let's call it A) can only be in one single package at once.
- If another unit (say, Z) needs to use it (A), the package for that unit (Z) must reference (in the requires section) the package that contains unit A. Unit A should not be included directly.

If there still are naming conflicts, rename the units until each name is unique.




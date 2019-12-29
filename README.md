# OpenSSL Binaries for Windows
Building OpenSSL appears to be quite complicated on Windows and requires a number of tools and stages whilst avoiding many pitfalls.

The instructions for the build were linked to from the OpenSSL Wiki instructions on building but the resource is no longer available. The most recent snapshot from the _Internet Archive's_ ***Wayback Machine*** is [here](https://web.archive.org/web/20190602004956/http://developer.covenanteyes.com/building-openssl-for-visual-studio).

## Obtaining the Source
The OpenSSL source is included in the `/src` folder as `git submodules`. A 64-bit and 32-bit directory is required as the build system leaves artifacts which can upset building of the other versions. The currently checked-out commit is the tagged-release `1_1_1d`.

## Build Tools
* An Installation of `Perl`
    - [Active Perl](https://www.activestate.com/products/perl/) (sign-up required) 
    - [Strawberry Perl](http://strawberryperl.com/) (was not originally recommended)
* Visual Studio (including the _MSVC `C` compiler and `NMAKE`_)
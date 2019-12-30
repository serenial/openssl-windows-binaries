# OpenSSL Binaries for Windows
Building OpenSSL appears to be quite complicated on Windows and requires a number of tools and stages whilst avoiding many pitfalls.

## Obtaining the Source
The OpenSSL source is included in the `/src` folder as `git submodules`. A 64-bit and 32-bit directory is required as the build system leaves artifacts which can upset building of the other versions. The currently checked-out commit is the tagged-release `1_1_1d`.

## Build Tools

The OpenSSL library makes use of PERL for configuration of builds and uses NASM to complete the build process so ensure the following tools are installed.

* [Active Perl](https://www.activestate.com/products/perl/)
* [The Netwide Assembler - NASM](https://nasm.us/)
* Visual Studio (2015 used for this build)

## Setting Up Tools
* The availability of a GC++ compiler on your `PATH` environmental-variable might cause problems. The easiest solution is to edit your `PATH` so that tools like `C:\MinWG` aren't found.

* Launch The Visual Studio Command Prompt.
    - Building requires a number of Visual Studio tools which are most easily accessed via the Visual Studio Visual Studio Command Prompt (VS2015 [x86 or x64] Native Tools Command Prompt)

* Ensure that `PERL` and `NASM` tools are correctly installed and that Visual Studio's `nmake` is available;

    - For `PERL` the command `perl -v` should yield something similar to:
        ```shell
            This is perl 5, version 28, subversion 1 (v5.28.1) built for MSWin32-x64-multi-thread
            (with 1 registered patch, see perl -V for more detail)
            
            ...etc.
        ```

    - For `NASM` the command `nasm -v` should give you information on the `NASM` version like:
        ```shell
        NASM version 2.14.02 compiled on Dec 26 2018
        ```

    - Finally `nmake` availability should be verified with the command `nmake /?`

     If these tools aren't found then ensure they are available on your `PATH` environmental-variable or you manually set the `PATH` variable in the command prompt session. If `nmake` is not found, check you are using the Visual Studio Command Prompt and consider re-installing Visual Studio.

* According to [NOTES.PERL](https://github.com/serenial/openssl/blob/master/NOTES.PERL) some additional PERL modules are also required. To install these modules use the `cpan` tool
```shell
 cpan -i Text::Template
 cpan -i Test::More <optional install>
```

## Building 32-bit Static Binaries
* Run Visual Studio Command Prompt (VS2015 x86 Native Tools Command Prompt)
* `cd` into the `src/32` directory
* Run the following commands
    ```shell
    perl Configure VC-WIN32
    nmake
    nmake test
    nmake install
    ```

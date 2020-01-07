# OpenSSLv1.1.1 Binaries for Windows
Building OpenSSL can be quite straight-forward with a fair wind but it is a somewhat manual process to get it all setup.

## Cloning This Repository
The OpenSSL source is included in the `/src` folder as `git submodules`. A 64-bit and 32-bit directory is required as the build system leaves artifacts which can upset building of the other versions. The currently checked-out commit is the tagged-release `1_1_1d`.

To clone this repository and its submodules, clone the main repository with:
```shell
git clone --recursive <GIT_REPO_URL>
```
And if you have already cloned the main repo then use:
```shell
git submodule init
git submodule update
```


## Build Tools

The OpenSSL library makes use of `PERL` for configuration of builds and uses `NASM` [The Netwide Assembler] to complete the build process so ensure the following tools are installed;

* [Strawberry Perl](http://strawberryperl.com/)
    - Active Perl should be suitable but I had issues installing perl modules with `cpan` as the MinGW tooling that Active Perl calls didn't install as expected so couldn't build the packages - maybe because I already have MinGW installed elsewhere. This means the perl-module installation would always fail.

* [NASM](https://nasm.us/)

* Visual Studio (2015 used for this build)

## Setting Up Tools
1. Launch The Visual Studio Command Prompt.
    - Building requires a number of Visual Studio tools which are most easily accessed via the Visual Studio Visual Studio Command Prompt (VS2015 [x86 or x64] Native Tools Command Prompt)

1. Ensure that `PERL` and `NASM` tools are correctly installed and that Visual Studio's `nmake` is available;

    - For `PERL` the command `perl -v` should yield something similar to:
        ```shell
            This is perl 5, version 30, subversion 1 (v5.30.1) built for MSWin32-x86-multi-thread-64int
            
            ...etc.
        ```

    - For `NASM` the command `nasm -v` should give you information on the `NASM` version like:
        ```shell
        NASM version 2.14.02 compiled on Dec 26 2018
        ```

    - Finally `nmake` availability should be verified with the command `nmake /?`

     If these tools aren't found then ensure they are available on your `PATH` environmental-variable or you manually set the `PATH` variable in the command prompt session. If `nmake` is not found, check you are using the Visual Studio Command Prompt and consider re-installing Visual Studio.

1. Instal the `PERL` modules as listed as required in [NOTES.PERL](https://github.com/serenial/openssl/blob/master/NOTES.PERL) with the `cpan` tool, which itself needs setting up if you haven't used it before.

    - To setup `cpan` open a command prompt with administrator-privileges and enter `cpan` to launch the interactive cpan command-line

    - Perform the automatic setup using  the command `o conf init`

    - Use the default options and follow the instructions to commit the changes to the config

    - Exit the `cpan` interactive command-line with the `quit` command

    - Install the required modules using:

        ```shell
        cpan -i Text::Template
        cpan -i Test::More <optional install>
        ```


## Building 64-bit Binaries
* Run Visual Studio Command Prompt (VS2015 **x64** Native Tools Command Prompt)

* `cd` into the `src/64` directory

* Run the following commands
    ```shell
    perl Configure VC-WIN64A --prefix=<ABSOLUTE_PATH_TO_INSTALL> --openssldir=<ABSOLUTE_PATH_TO_INSTALL>
    nmake
    nmake test
    nmake install #(requires a command prompt with administrator-privileges)
    ```

## Building 32-bit Binaries
* Run Visual Studio Command Prompt (VS2015 **x86** Native Tools Command Prompt)
* ensure that the `rc.exe` tool from the x86 Windows Kit is accessible (I added `C:\Program Files (x86)\Windows Kits\10\bin\10.0.18362.0\x86` to my path user-variable)
* `cd` into the `src/32` directory

* Run the following commands
    ```shell
    perl Configure VC-WIN32 --prefix=<ABSOLUTE_PATH_TO_INSTALL> --openssldir=<ABSOLUTE_PATH_TO_INSTALL>
    nmake
    nmake test
    nmake install #(requires a command prompt with administrator-privileges)
    ```
    
## Additional Resources
* [Detailed Instructions and Pre-Compiled Versions](http://www.p-nand-q.com/programming/windows/building_openssl_with_visual_studio_2013.html)

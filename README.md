Bundle MAGIC and JEDI base packages
===================================

Build bundle of base packages for MAGIC and JEDI application

Requirements
------------

Tested compilers include:

- GCC 7.3.0, 7.4.0
- Intel 17.x.y.z

Required dependencies:

- NetCDF (Fortran and CXX API)
- CMake
- ecbuild
- eckit
- fckit
- ATLAS
- SABER
- OOPS
- IODA
- UFO


Building the MAGIC bundle
-------------------------

MAGIC employs an out-of-source build/install based on CMake.

Make sure the ecbuild executable script is found ( `which ecbuild` ).

```bash
# 1. Clone the MAGIC-bundle
git clone https://github.com/aerorahul/magic-bundle.git
cd magic-bundle

# 2. Create the build directory and cd into it:
mkdir /path/to/build
cd /path/to/build

# 3. Run ecbuild:
ecbuild /path/to/magic-bundle

# 4. Compile / Install
make -j 10
make install
```

Extra flags maybe added to `ecbuild` in step 3 to fine-tune configuration.

- `--build=DEBUG|RELEASE|BIT` --- Optimisation level
  * DEBUG:   No optimisation (`-O0 -g`)
  * BIT:     Maximum optimisation while remaning bit-reproducible (`-O2 -g`)
  * RELEASE: Maximum optimisation (`-O3`)

- compilers can be selected with `-DCMAKE_CXX_COMPILER=/path/to/gcc-7.2/bin/g++`

The `ecbuild` command in step 3 will clone all the source code for the JEDI and MAGIC project defined in the
`CMakeLists.txt` in the bundle and the make command in step 4 will build them all.

Testing
-------

For testing (from build directory):

```bash
ctest
```

Working with the code
---------------------

The `CMakeLists.txt` file in this directory contains the list of the repositories included
in the bundle and the branch to be used. The branch specified in the CMakeLists.txt is
the one that will be compiled. When working with you own branch, the should be changed in
the `CMakeLists.txt` file but it is not necessary to re-run ecbuild, make is enough.

After the fisrt build, changes in the code can be tested by re-running only
(from build directory):

```bash
make -j4
ctest
```

By default, make will not update your local repository from the remote. To update all repositories
in the bundle, run:

```bash
make update
```

The update will fail for repositories that contain uncommited code. This is a safety mechanism to
avoid losing your work.

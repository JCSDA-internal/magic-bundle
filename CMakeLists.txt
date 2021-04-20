# (C) Copyright 2019-2021 NOAA/NWS/NCEP/EMC.
#
# This software is licensed under the terms of the Apache Licence Version 2.0
# which can be obtained at http://www.apache.org/licenses/license-2.0.

#
# MAGIC bundle
#

cmake_minimum_required( VERSION 3.3.2 FATAL_ERROR )

find_package( ecbuild 3.5 REQUIRED )

project( magic-bundle VERSION 0.0.1 LANGUAGES C CXX Fortran )

list( APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake )
include( ecbuild_bundle )

set( ECBUILD_DEFAULT_BUILD_TYPE Release )
set( ENABLE_MPI ON CACHE BOOL "Compile with MPI" )

ecbuild_bundle_initialize()

ecbuild_requires_macro_version( 2.7 )

ecbuild_add_option( FEATURE OMP
                    DEFAULT OFF
                    DESCRIPTION "Use OpenMP" )

ecbuild_bundle( PROJECT jedicmake GIT "https://github.com/jcsda-internal/jedi-cmake.git" BRANCH develop UPDATE )

find_package( eckit QUIET 1.16.0 )
if( NOT eckit_FOUND )
  ecbuild_bundle( PROJECT eckit GIT "https://github.com/ecmwf/eckit.git" UPDATE TAG 1.16.0 )
endif()

find_package( fckit QUIET 0.9.2  )
if( NOT fckit_FOUND )
  ecbuild_bundle( PROJECT fckit GIT "https://github.com/ecmwf/fckit.git" UPDATE TAG 0.9.2 )
endif()

find_package( atlas QUIET 0.23.0 )
if( NOT atlas_FOUND )
  ecbuild_bundle( PROJECT atlas GIT "https://github.com/ecmwf/atlas.git" UPDATE TAG 0.23.0 )
endif()

ecbuild_bundle( PROJECT oops  GIT "https://github.com/JCSDA-Internal/oops.git"  UPDATE BRANCH develop )
ecbuild_bundle( PROJECT saber GIT "https://github.com/JCSDA-Internal/saber.git" UPDATE BRANCH develop )
ecbuild_bundle( PROJECT ioda  GIT "https://github.com/JCSDA-Internal/ioda.git"  UPDATE BRANCH develop )
ecbuild_bundle( PROJECT ufo   GIT "https://github.com/JCSDA-Internal/ufo.git"   UPDATE BRANCH develop )

ecbuild_bundle( PROJECT magic GIT "https://github.com/JCSDA-Internal/magic.git" UPDATE BRANCH develop )

ecbuild_bundle_finalize()

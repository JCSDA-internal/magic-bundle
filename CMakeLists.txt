# (C) COPYRIGHT 2019-2019.
#
# THIS SOFTWARE IS LICENSED UNDER THE TERMS OF THE APACHE LICENCE VERSION 2.0
# WHICH CAN BE OBTAINED AT HTTP://WWW.APACHE.ORG/LICENSES/LICENSE-2.0.

#
# MAGIC-BUNDLE
#

project( magic-bundle C CXX Fortran )

cmake_minimum_required( VERSION 3.3.2 FATAL_ERROR )

list( APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake )
include( ecbuild_bundle )

set( ECBUILD_DEFAULT_BUILD_TYPE Release )
set( ENABLE_MPI ON CACHE BOOL "Compile with MPI" )

ecbuild_bundle_initialize()

ecbuild_requires_macro_version( 2.7 )

#ecbuild_add_option( FEATURE OMP
#                    DEFAULT ON
#                    DESCRIPTION "Use OpenMP" )

ecbuild_add_option( FEATURE BUILD_ECKIT
                    DEFAULT OFF
                    DESCRIPTION "download and build eckit (not needed if loaded by module or in a JEDI container)" )

ecbuild_add_option( FEATURE BUILD_FCKIT
                    DEFAULT OFF
                    DESCRIPTION "download and build fckit (not needed if loaded by module or in a JEDI container)" )

ecbuild_add_option( FEATURE BUILD_ATLAS
                    DEFAULT OFF
                    DESCRIPTION "download and build atlas (not needed if loaded by module or in a JEDI container)" )

if( BUILD_ECKIT )
  ecbuild_bundle( PROJECT eckit GIT "https://github.com/JCSDA/eckit.git" UPDATE BRANCH develop )
endif()

if( BUILD_FCKIT )
  ecbuild_bundle( PROJECT fckit GIT "https://github.com/JCSDA/fckit.git" UPDATE BRANCH develop )
endif()

if( BUILD_ATLAS )
  ecbuild_bundle( PROJECT atlas GIT "https://github.com/JCSDA/atlas.git" UPDATE BRANCH develop )
endif()

ecbuild_bundle( PROJECT saber GIT "https://github.com/JCSDA/saber.git" UPDATE BRANCH develop )
ecbuild_bundle( PROJECT oops  GIT "https://github.com/JCSDA/oops.git"  UPDATE BRANCH develop )
ecbuild_bundle( PROJECT ioda  GIT "https://github.com/JCSDA/ioda.git"  UPDATE BRANCH develop )
ecbuild_bundle( PROJECT ufo   GIT "https://github.com/JCSDA/ufo.git"   UPDATE BRANCH develop )

ecbuild_bundle( PROJECT magic GIT "https://github.com/aerorahul/magic.git" UPDATE BRANCH develop )

ecbuild_bundle_finalize()

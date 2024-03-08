cmake_minimum_required(VERSION 3.26)

project(3rdPartyLibs)

include(FetchContent)
include(ExternalProject)

if (WIN32)
set (CMAKE_INSTALL_PREFIX    /FoVI3D/3rdPartyLibs)
endif (WIN32)

set (CMAKE_DEBUG_POSTFIX      d)
set (CMAKE_CXX_STANDARD       17)

set (CMAKE_MODULE_PATH        ${CMAKE_INSTALL_PREFIX}/cmake
                              ${CMAKE_INSTALL_PREFIX}/lib/cmake
                              )

set (CMAKE_PREFIX_PATH        ${CMAKE_INSTALL_PREFIX}/cmake
                              ${CMAKE_INSTALL_PREFIX}/lib/cmake
                              )

set (ALLOW_DUPLICATE_CUSTOM_TARGETS OFF)

if (UNIX)
set(CMAKE_C_COMPILER                      /usr/bin/gcc-8 CACHE PATH "" FORCE)
set(CMAKE_CXX_COMPILER                    /usr/bin/g++-8 CACHE PATH "" FORCE)
set(CMAKE_CXX_FLAGS                       "-fPIC")
set(CMAKE_CXX_FLAGS_DEBUG                 "-g")
set(CMAKE_CXX_FLAGS_RELEASE               "-O3")  
endif (UNIX)


#------------------------------------------------------------------------------
# Options
# sudo make install InstallFlann InstallUSB
option(BUILD3rd_Group1           "Build Group 1 Libraries"   OFF)
option(BUILD3rd_Group2           "Build Group 2 Libraries"   OFF)
option(BUILD3rd_Group3           "Build Group 3 Libraries"   OFF)
option(BUILD3rd_Group4           "Build Group 4 Libraries"   OFF)
option(BUILD3rd_Group5           "Build Group 5 Libraries"   On)
option(BUILD3rd_Group6           "Build Group 6 Libraries"   OFF) 

# Group 1
option(BUILD3rd_zLib             "Build zLib"                OFF)     
option(BUILD3rd_VCPkg            "Build VCPkg"               OFF)     
option(BUILD3rd_GLM              "Build GLM"                 OFF)   
option(BUILD3rd_GLEW             "Build GLEW"                OFF)   
option(BUILD3rd_GLFW             "Build GLFW"                OFF)       
option(BUILD3rd_GLUT             "Build GLUT"                OFF)     
option(BUILD3rd_USB              "Build USB"                 OFF)     
option(BUILD3rd_FreeType         "Build FreeType"            OFF)     
option(BUILD3rd_Sodium           "Build Sodium"              OFF)     
option(BUILD3rd_FlatBuffers      "Build FlatBuffers"         OFF)     
option(BUILD3rd_JSon             "Build nLohmann JSon"       OFF)     
option(BUILD3rd_ZMQ              "Build ZMQ"                 OFF)     
option(BUILD3rd_Flann            "Build Flann"               OFF)   # make InstallFlann
# Group 2
option(BUILD3rd_HDF5             "Build HDF5"                OFF)   # Needs to be build by itself
# Group 3
option(BUILD3rd_Eigen            "Build Eigen"               OFF)     
# Group 4
option(BUILD3rd_SDL              "Build SDL"                 OFF) 
option(BUILD3rd_VTK              "Build VTK"                 OFF)     
# Group 5
option(BUILD3rd_OpenCV           "Build OpenCV"              OFF)      
option(BUILD3rd_Bullet           "Build Bullet"              OFF)     
option(BUILD3rd_Assimp           "Build Assimp"              OFF)     
# Group 6
option(BUILD3rd_CvPlot           "Build CvPlot"              OFF)     
option(BUILD3rd_PCL              "Build PCL"                 OFF)     
# Group 7
option(BUILD3rd_RealSense        "Build RealSense"           OFF)   # uninstall target conflict 


option(BUILD3rd_CZMQ             "Build CZMQ"                OFF) 
#------------------------------------------------------------------------------


#------------------------------------------------------------------------------
# Message setttings
message ("")
message ("CMAKE_INSTALL_PREFIX:   " ${CMAKE_INSTALL_PREFIX})
message ("CMAKE_SOURCE_DIR:       " ${CMAKE_SOURCE_DIR})
message ("FETCHCONTENT_BASE_DIR:  " ${FETCHCONTENT_BASE_DIR})
message ("CMAKE_MODULE_PATH:      " ${CMAKE_MODULE_PATH})
message ("CMAKE_PREFIX_PATH:      " ${CMAKE_PREFIX_PATH})
message ("")
#------------------------------------------------------------------------------


# zLib
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_zLIB)
  message ("")
  message ("Add zLib to Build") 

  FetchContent_Declare(
    zLib
    GIT_REPOSITORY  https://github.com/madler/zlib.git
    GIT_TAG         51b7f2abdade71cd9bb0e7a373ef2610ec6f9daf # release 1.3.1
  )

  FetchContent_MakeAvailable(zLib)

  message ("Add Build zLib Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_zLIB)
#------------------------------------------------------------------------------



# VCPkg
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_VCPkg)
  message ("")
  message ("Add VCPkg to Build") 

  FetchContent_Declare(
    VCPkg
    GIT_REPOSITORY  https://github.com/microsoft/vcpkg.git
    GIT_TAG         fba75d09065fcc76a25dcf386b1d00d33f5175af # release 2024.2.14
  )

  FetchContent_MakeAvailable(VCPkg)

  message ("Add Build VCPkg Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_VCPkg)
#------------------------------------------------------------------------------


# GLM
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_GLM)
  message ("")
  message("Add GLM to Build")

  set (GLM_BUILD_INSTALL ON)

  FetchContent_Declare(
    glm
    GIT_REPOSITORY https://github.com/g-truc/glm.git
    GIT_TAG        0af55ccecd98d4e5a8d1fad7de25ba429d60e863 # release-1.0.1
  )

  FetchContent_MakeAvailable(glm)

  message ("Add Build GLM Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_GLM)
#------------------------------------------------------------------------------


# GLEW
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_GLEW)
  message ("")
  message("Add GLEW to Build")

  FetchContent_Declare(
    GLEW
    GIT_REPOSITORY https://github.com/edoren/glew.git
    GIT_TAG        5b995cab14f97231b48bc86b447be5e23b899626 # release-2.0.0
  )

  FetchContent_MakeAvailable(GLEW)
  add_subdirectory(${FETCHCONTENT_BASE_DIR}/glew-src/build/cmake)

  message ("Add Build GLEW Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_GLEW)
#------------------------------------------------------------------------------


# GLFW
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_GLFW)
  message ("")
  message("Add GLFW to Build")

  FetchContent_Declare(
    GLFW
    GIT_REPOSITORY https://github.com/glfw/glfw.git
    GIT_TAG        7b6aead9fb88b3623e3b3725ebb42670cbe4c579 # release-3.4.0
  )

  FetchContent_MakeAvailable(GLFW)

  message ("Add Build GLFW Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_GLFW)
#------------------------------------------------------------------------------


# GLUT
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_GLUT)
  include(Inc/GLUT.txt)
endif (BUILD3rd_Group1 OR BUILD3rd_GLUT)
#------------------------------------------------------------------------------


# USB
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_USB)
  include(Inc/USB.txt)
endif (BUILD3rd_Group1 OR BUILD3rd_USB)
#------------------------------------------------------------------------------


# FreeType
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_FreeType)
  message ("")
  message("Add FreeType to Build")

  FetchContent_Declare(
    FreeType
    GIT_REPOSITORY https://gitlab.freedesktop.org/freetype/freetype.git
    GIT_TAG        920c5502cc3ddda88f6c7d85ee834ac611bb11cc # release-2.13.2
  )

  FetchContent_MakeAvailable(FreeType)
  
  message ("Add Build FreeType Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_FreeType)
#------------------------------------------------------------------------------


# Sodium
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_Sodium)
  include(Inc/Sodium.txt)
endif (BUILD3rd_Group1 OR BUILD3rd_Sodium)
#------------------------------------------------------------------------------


# FlatBuffers
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_FlatBuffers)
  message ("")
  message("Add FlatBuffers to Build")

  FetchContent_Declare(
    FlatBuffers
    GIT_REPOSITORY https://github.com/google/flatbuffers.git
    GIT_TAG        0100f6a5779831fa7a651e4b67ef389a8752bd9b # release-23.5.26
  )

  FetchContent_MakeAvailable(FlatBuffers)

  message ("Add Build FlatBuffers Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_FlatBuffers)
#------------------------------------------------------------------------------


# nLohmann JSon
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_JSon)
  message ("")
  message("Add JSon to Build")

  FetchContent_Declare(
    JSon
    GIT_REPOSITORY https://github.com/nlohmann/json.git
    GIT_TAG        9cca280a4d0ccf0c08f47a99aa71d1b0e52f8d03 # release-3.11.1
  )

  set (JSON_Install     ON)

  FetchContent_MakeAvailable(JSon)

  message ("Add Build JSon Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_JSon)
#------------------------------------------------------------------------------


# ZMQ
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_ZMQ)
  message ("")
  message("Add ZMQ to Build")

  FetchContent_Declare(
    ZMQ
    GIT_REPOSITORY https://github.com/zeromq/libzmq.git
    GIT_TAG        622fc6dde99ee172ebaa9c8628d85a7a1995a21d # release-4.3.5
  )

  FetchContent_MakeAvailable(ZMQ)

  message ("Add Build ZMQ Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_ZMQ)
#------------------------------------------------------------------------------


# Flann
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_Flann)
  message ("")
  message ("Add Flann to Build") 

  FetchContent_Declare(
    Flann
    GIT_REPOSITORY https://github.com/flann-lib/flann.git
    GIT_TAG        06a49513138009d19a1f4e0ace67fbff13270c69 # release 1.9.1
  )

  set (BUILD_C_BINDINGS         OFF)
  set (BUILD_PYTHON_BINDINGS    OFF)
  set (BUILD_MATLAB_BINDINGS    OFF)
  set (BUILD_CUDA_LIB           OFF)
  set (BUILD_EXAMPLES           OFF)
  set (BUILD_TESTS              OFF)
  set (BUILD_DOC                OFF)
  set (USE_OPENMP               OFF)
  set (USE_MPI                  OFF)

  FetchContent_Populate(Flann)
  add_custom_target("InstallFlann")
  add_custom_command(TARGET "InstallFlann"    
                     COMMAND ${CMAKE_COMMAND} -E copy_directory
                     ${FETCHCONTENT_BASE_DIR}/flann-src/src/cpp/flann ${CMAKE_INSTALL_PREFIX}/include/flann)       

  message ("Add Build Flann Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_Flann)
#------------------------------------------------------------------------------


# HDF5
#------------------------------------------------------------------------------
if (BUILD3rd_Group2 OR BUILD3rd_HDF5)
  message ("")
  message ("Add HDF5 to Build") 

  FetchContent_Declare(
    HDF5
    GIT_REPOSITORY  https://github.com/HDFGroup/hdf5.git
    GIT_TAG         8b5cac6bc498546efa5639f99bb7dbbc1a2d5d90 # release 1.14.3
  )
  
  FetchContent_MakeAvailable(HDF5)
  
  message ("Add Build HDF5 Finished")
  message ("")
endif (BUILD3rd_Group2 OR BUILD3rd_HDF5)
#------------------------------------------------------------------------------


# CZMQ
#------------------------------------------------------------------------------
if (BUILD3rd_GroupN OR BUILD3rd_CZMQ)
  include(Inc/CZMQ.txt)
endif (BUILD3rd_GroupN OR BUILD3rd_CZMQ)
#------------------------------------------------------------------------------


# Eigen
#------------------------------------------------------------------------------
if (BUILD3rd_Group3 OR BUILD3rd_Eigen)
  include(Inc/Eigen.txt)
endif (BUILD3rd_Group3 OR BUILD3rd_Eigen)
#------------------------------------------------------------------------------


# SDL
#------------------------------------------------------------------------------
if (BUILD3rd_Group4 OR BUILD3rd_SDL)
  include(Inc/SDL.txt)
endif (BUILD3rd_Group4 OR BUILD3rd_SDL)
#------------------------------------------------------------------------------


# VTK
#------------------------------------------------------------------------------
if (BUILD3rd_Group4 OR BUILD3rd_VTK)
  include(Inc/VTK.txt)
endif (BUILD3rd_Group4 OR BUILD3rd_VTK)
#------------------------------------------------------------------------------


# OpenCV
#------------------------------------------------------------------------------
if (BUILD3rd_Group5 OR BUILD3rd_OpenCV)
  include(Inc/OpenCV.txt)
endif (BUILD3rd_Group5 OR BUILD3rd_OpenCV)
#------------------------------------------------------------------------------


# Bullet
#------------------------------------------------------------------------------
if (BUILD3rd_Group5 OR BUILD3rd_Bullet)
  include(Inc/Bullet.txt)
endif (BUILD3rd_Group5 OR BUILD3rd_Bullet)
#------------------------------------------------------------------------------


# Assimp
#------------------------------------------------------------------------------
if (BUILD3rd_Group5 OR BUILD3rd_Assimp)
  include(Inc/Assimp.txt)
endif (BUILD3rd_Group5 OR BUILD3rd_Assimp)
#------------------------------------------------------------------------------


# CvPlot
#------------------------------------------------------------------------------
if (BUILD3rd_Group8 OR BUILD3rd_CvPlot)
  message ("")
  message("Add CvPlot to Build")
 
  FetchContent_Declare(
    CvPlot
    GIT_REPOSITORY https://github.com/Profactor/cv-plot.git
    GIT_TAG        92ea307137e1abc3d49a5018ef80f4fbf189196b # release-1.2.2
  )

  set (CVPLOT_USE_CONAN OFF)  

  FetchContent_MakeAvailable(CvPlot)

  target_compile_options(CvPlot -DCVPLOT_USE_CONAN=OFF) 

  message ("Add Build CvPlot Finished")
  message ("")
endif (BUILD3rd_Group8 OR BUILD3rd_CvPlot)
#------------------------------------------------------------------------------


# PCL
#------------------------------------------------------------------------------
if (BUILD3rd_Group6 OR BUILD3rd_PCL)
  message ("")
  message("Add PCL to Build")
 
  FetchContent_Declare(
    PCL
    GIT_REPOSITORY https://github.com/PointCloudLibrary/pcl.git
    GIT_TAG        f62c018b4fc7df3dc2c096918a8462a190f28bb8 # release-1.14.0
  )

  set (WITH_VTK   OFF)
  set (WITH_CUDA  OFF)

  FetchContent_MakeAvailable(PCL)

  message ("Add Build PCL Finished")
  message ("")
endif (BUILD3rd_Group6 OR BUILD3rd_PCL)

#------------------------------------------------------------------------------


# RealSense
#------------------------------------------------------------------------------
if (BUILD3rd_Group7 OR BUILD3rd_RealSense)
  message ("")
  message("Add RealSense to Build")
 
  FetchContent_Declare(
    RealSense
    GIT_REPOSITORY https://github.com/IntelRealSense/librealsense.git
    GIT_TAG        2dbaaf5964490cb02f811cf2ed38c8a893f5c027 # release-2.54.2
  )

  FetchContent_Populate(RealSense)

  set (BUILD_SHARED_LIBS          ON)
  set (BUILD_EXAMPLES             OFF)
  set (BUILD_GRAPHICAL_EXAMPLES   OFF)
  set (BUILD_GLFW                 OFF)

  add_subdirectory(${FETCHCONTENT_BASE_DIR}/realsense-src ${FETCHCONTENT_BASE_DIR}/realsense-build)

  #FetchContent_MakeAvailable(RealSense)


  message ("Add Build RealSense Finished")
  message ("")
endif (BUILD3rd_Group7 OR BUILD3rd_RealSense)
#------------------------------------------------------------------------------


# Message
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_Flann)
message ("To Finish installing Flann: sudo make InstallFlann")
endif (BUILD3rd_Group1 OR BUILD3rd_Flann)

message("")
message("")



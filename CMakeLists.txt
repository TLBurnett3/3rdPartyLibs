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
#set(CMAKE_C_COMPILER                      /usr/bin/gcc-8 CACHE PATH "" FORCE)
#set(CMAKE_CXX_COMPILER                    /usr/bin/g++-8 CACHE PATH "" FORCE)
set(CMAKE_CXX_FLAGS_DEBUG                 "-g")
set(CMAKE_CXX_FLAGS_RELEASE               "-O3")  
endif (UNIX)


#------------------------------------------------------------------------------
# Options
option(BUILD3rd_Group1           "Build Group 1 Libraries"   ON)
option(BUILD3rd_Group2           "Build Group 2 Libraries"   OFF)
option(BUILD3rd_Group3           "Build Group 3 Libraries"   OFF)
option(BUILD3rd_Group4           "Build Group 4 Libraries"   OFF)
option(BUILD3rd_Group5           "Build Group 5 Libraries"   OFF)

option(BUILD3rd_zLib             "Build zLib"                OFF)     # 1
option(BUILD3rd_VCPkg            "Build VCPkg"               OFF)     # 1
option(BUILD3rd_GLM              "Build GLM"                 OFF)     # 1
option(BUILD3rd_GLFW             "Build GLFW"                OFF)     # 1
option(BUILD3rd_GLEW             "Build GLEW"                OFF)     # 1
option(BUILD3rd_FreeType         "Build FreeType"            OFF)     # 1
option(BUILD3rd_LibSodium        "Build LibSodium"           OFF)     # 1
option(BUILD3rd_FlatBuffers      "Build FlatBuffers"         OFF)     # 1
option(BUILD3rd_JSon             "Build nLohmann JSon"       OFF)     # 1
option(BUILD3rd_ZMQ              "Build ZMQ"                 OFF)     # 1
option(BUILD3rd_Flann            "Build Flann"               OFF)     # 1
option(BUILD3rd_HDF5             "Build HDF5"                OFF)     # 2
option(BUILD3rd_VTK              "Build VTK"                 OFF)     # 3
option(BUILD3rd_Eigen            "Build Eigen"               OFF)     # 4
option(BUILD3rd_Bullet           "Build Bullet"              OFF)     # 5
option(BUILD3rd_OpenCV           "Build OpenCV"              OFF)     # 5
option(BUILD3rd_Assimp           "Build Assimp"              OFF)     # 5
option(BUILD3rd_PCL              "Build PCL"                 OFF)     # 5
option(BUILD3rd_CvPlot           "Build CvPlot"              OFF)     # 5
option(BUILD3rd_RealSense        "Build RealSense"           OFF)     # 5
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
if (BUILD3rd_Group1 OR BUILD3rd_zLib)
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
endif (BUILD3rd_Group1 OR BUILD3rd_zLib)
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


# LibSodium
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_LibSodium)
  message ("")
  message("Add LibSodium to Build")

  FetchContent_Declare(
    LibSodium
    GIT_REPOSITORY https://github.com/jedisct1/libsodium.git
    GIT_TAG        fb4533b0a941b3a5b1db5687d1b008a5853d1f29 # release-1.0.19
  )

  FetchContent_MakeAvailable(LibSodium)
  ExternalProject_Add(LibSodium
                      SOURCE_DIR ${FETCHCONTENT_BASE_DIR}/libsodium-src
                      CONFIGURE_COMMAND ${FETCHCONTENT_BASE_DIR}/libsodium-src/configure
                      BUILD_COMMAND make install
                      BUILD_IN_SOURCE 1
                      )
                    #add_custom_command(OUTPUT  ${FETCHCONTENT_BASE_DIR}/libsodium-src/Makefile
  #                 COMMAND make install
  #                 WORKING_DIRECTORY ${FETCHCONTENT_BASE_DIR}/libsodium-src)
  
  message ("Add Build LibSodium Finished")
  message ("")
endif (BUILD3rd_Group1 OR BUILD3rd_LibSodium)
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
#    GIT_SHALLOW    ON
  )

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


# Eigen
#------------------------------------------------------------------------------
if (BUILD3rd_Eigen)
  message ("")
  message("Add Eigen to Build")

  FetchContent_Declare(
    Eigen
    GIT_REPOSITORY https://gitlab.com/libeigen/eigen.git
    #GIT_TAG        0fd6b4f71dd85b2009ee4d1aeb296e2c11fc9d68 # release-3.3.9
  )

  FetchContent_MakeAvailable(Eigen)

  message ("Add Build Eigen Finished")
  message ("")
endif (BUILD3rd_Eigen)
#------------------------------------------------------------------------------


# HDF5
#------------------------------------------------------------------------------
if (BUILD3rd_HDF5)
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
endif (BUILD3rd_HDF5)
#------------------------------------------------------------------------------



# OpenCV
#------------------------------------------------------------------------------
if (BUILD3rd_OpenCV)
  message ("")
  message ("Add OpenCV to Build") 

  FetchContent_Declare(
    OpenCV_Contrib
    GIT_REPOSITORY  https://github.com/opencv/opencv_contrib.git
    GIT_TAG         c7602a8f74205e44389bd6a4e8d727d32e7e27b4 # release 4.9.0
  )

  FetchContent_MakeAvailable(OpenCV_Contrib)

  FetchContent_Declare(
    OpenCV
    GIT_REPOSITORY  https://github.com/opencv/opencv.git
    GIT_TAG         dad8af6b17f8e60d7b95a1203a1b4d22f56574cf # release 4.9.0
  )
  
  set (OPENCV_EXTRA_MODULES_PATH      ${FETCHCONTENT_BASE_DIR}/opencv_contrib-src/modules)
  set (WITH_GSTREAMER                 OFF)
  set (BUILD_EXAMPLES                 OFF)
  set (BUILD_opencv_java              OFF)
  set (BUILD_opencv_python            OFF)
  set (BUILD_opencv_hdf               OFF)  

  FetchContent_MakeAvailable(OpenCV)

  message ("Add Build OpenCV Finished")
  message ("")
endif (BUILD3rd_OpenCV)
#------------------------------------------------------------------------------


# CvPlot
#------------------------------------------------------------------------------
if (BUILD3rd_CvPlot)
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
endif (BUILD3rd_CvPlot)
#------------------------------------------------------------------------------


# RealSense
#------------------------------------------------------------------------------
if (BUILD3rd_RealSense)
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
endif (BUILD3rd_RealSense)
#------------------------------------------------------------------------------


# Bullet
#------------------------------------------------------------------------------
if (BUILD3rd_Bullet)
  message ("")
  message("Add Bullet to Build")
 
  FetchContent_Declare(
    Bullet
    GIT_REPOSITORY https://github.com/bulletphysics/bullet3.git
    GIT_TAG        2c204c49e56ed15ec5fcfa71d199ab6d6570b3f5 # release-3.2.5
  )

  set (BUILD_UNIT_TESTS                 OFF)
  set (INSTALL_LIBS                     ON)

  FetchContent_MakeAvailable(Bullet)

  message ("Add Build Bullet Finished")
  message ("")
endif (BUILD3rd_Bullet)
#------------------------------------------------------------------------------


# Assimp
#------------------------------------------------------------------------------
if (BUILD3rd_Assimp)
  message ("")
  message("Add Assimp to Build")
 
  FetchContent_Declare(
    Assimp
    GIT_REPOSITORY https://github.com/assimp/assimp.git
    GIT_TAG        6a08c39e3a91ef385e76515cfad86aca4bfd57ff # release-5.3.1
  )

  FetchContent_MakeAvailable(Assimp)

  message ("Add Build Assimp Finished")
  message ("")
endif (BUILD3rd_Assimp)
#------------------------------------------------------------------------------


# VTK
#------------------------------------------------------------------------------
if (BUILD3rd_VTK)
  message ("")
  message("Add VTK to Build")
 
  FetchContent_Declare(
    VTK
    GIT_REPOSITORY https://gitlab.kitware.com/vtk/vtk.git
    GIT_TAG        357d9efeed29cba6383ce626575f1a5f1ac1eefb # release-9.3.0
  )

  FetchContent_MakeAvailable(VTK)
  
  message ("Add Build VTK Finished")
  message ("")
endif (BUILD3rd_VTK)
#------------------------------------------------------------------------------


# PCL
#------------------------------------------------------------------------------
if (BUILD3rd_PCL)
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
endif (BUILD3rd_PCL)
#------------------------------------------------------------------------------


# Message
#------------------------------------------------------------------------------
if (BUILD3rd_Flann)
message ("To Finish installing Flann: sudo make InstallFlann")
endif (BUILD3rd_Flann)

message("")
message("")



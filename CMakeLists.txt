cmake_minimum_required(VERSION 3.26)

project(3rdPartyLibs)

include(FetchContent)

if (WIN32)
set (CMAKE_INSTALL_PREFIX    /FoVI3D/3rdPartyLibs)
endif (WIN32)

set (CMAKE_DEBUG_POSTFIX      d)
set (CMAKE_CXX_STANDARD       17)
set (CMAKE_MODULE_PATH        ${CMAKE_INSTALL_PREFIX}/cmake)
set (CMAKE_PREFIX_PATH        ${CMAKE_INSTALL_PREFIX}/cmake)


#------------------------------------------------------------------------------
# Options
option(BUILD3rd_zLib             "Build zLib"                OFF)
option(BUILD3rd_VCPkg            "Build VCPkg"               OFF)
option(BUILD3rd_GLM              "Build GLM"                 OFF)
option(BUILD3rd_FlatBuffers      "Build FlatBuffers"         OFF)
option(BUILD3rd_JSon             "Build nLohmann JSon"       OFF)
option(BUILD3rd_ZMQ              "Build ZMQ"                 OFF)
option(BUILD3rd_OpenCV           "Build OpenCV"              OFF)
option(BUILD3rd_CvPlot           "Build CvPlot"              OFF)
option(BUILD3rd_Eigen            "Build Eigen"               OFF)
option(BUILD3rd_Flann            "Build Flann"               OFF)
option(BUILD3rd_HDF5             "Build HDF5"                OFF)
#------------------------------------------------------------------------------



#------------------------------------------------------------------------------
# Message setttings
message ("")
message ("CMAKE_SOURCE_DIR:       " ${CMAKE_SOURCE_DIR})
message ("FETCHCONTENT_BASE_DIR:  " ${FETCHCONTENT_BASE_DIR})
message ("CMAKE_MODULE_PATH:      " ${CMAKE_MODULE_PATH})
message ("CMAKE_PREFIX_PATH:      " ${CMAKE_PREFIX_PATH})
message ("")
#------------------------------------------------------------------------------


# zLib
#------------------------------------------------------------------------------
if (BUILD3rd_zLib)
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
endif (BUILD3rd_zLib)
#------------------------------------------------------------------------------



# VCPkg
#------------------------------------------------------------------------------
if (BUILD3rd_VCPkg)
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
endif (BUILD3rd_VCPkg)
#------------------------------------------------------------------------------


# GLM
#------------------------------------------------------------------------------
if (BUILD3rd_GLM)
  message ("")
  message("Downloading GLM")
  set (GLM_BUILD_INSTALL ON)
  FetchContent_Declare(
    glm
    GIT_REPOSITORY https://github.com/g-truc/glm.git
    GIT_TAG        0af55ccecd98d4e5a8d1fad7de25ba429d60e863 # release-1.0.1
  )
  FetchContent_MakeAvailable(glm)
  message ("Downloading GLM Finished")
  message ("")
endif (BUILD3rd_GLM)
#------------------------------------------------------------------------------


# FlatBuffers
#------------------------------------------------------------------------------
if (BUILD3rd_FlatBuffers)
  message ("")
  message("Downloading FlatBuffers")
  FetchContent_Declare(
    FlatBuffers
    GIT_REPOSITORY https://github.com/google/flatbuffers.git
    GIT_TAG        0100f6a5779831fa7a651e4b67ef389a8752bd9b # release-23.5.26
  )
  FetchContent_MakeAvailable(FlatBuffers)
  message ("Downloading FlatBuffers Finished")
  message ("")
endif (BUILD3rd_FlatBuffers)
#------------------------------------------------------------------------------


# nLohmann JSon
#------------------------------------------------------------------------------
if (BUILD3rd_JSon)
  message ("")
  message("Downloading JSon")
  FetchContent_Declare(
    JSon
    GIT_REPOSITORY https://github.com/nlohmann/json.git
    GIT_TAG        9cca280a4d0ccf0c08f47a99aa71d1b0e52f8d03 # release-3.11.1
    GIT_SHALLOW    ON
  )
  FetchContent_MakeAvailable(JSon)
  message ("Downloading JSon Finished")
  message ("")
endif (BUILD3rd_JSon)
#------------------------------------------------------------------------------


# ZMQ
#------------------------------------------------------------------------------
if (BUILD3rd_ZMQ)
  message ("")
  message("Downloading ZMQ")
  FetchContent_Declare(
    ZMQ
    GIT_REPOSITORY https://github.com/zeromq/libzmq.git
    GIT_TAG        622fc6dde99ee172ebaa9c8628d85a7a1995a21d # release-4.3.5
  )
  FetchContent_MakeAvailable(ZMQ)
  message ("Downloading ZMQ Finished")
  message ("")
endif (BUILD3rd_ZMQ)
#------------------------------------------------------------------------------


# Eigen
#------------------------------------------------------------------------------
if (BUILD3rd_Eigen)
  message ("")
  message("Downloading Eigen")
  FetchContent_Declare(
    Eigen
    GIT_REPOSITORY https://gitlab.com/libeigen/eigen.git
    #GIT_TAG        0fd6b4f71dd85b2009ee4d1aeb296e2c11fc9d68 # release-3.3.9
  )
  FetchContent_MakeAvailable(Eigen)
  message ("Downloading Eigen Finished")
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



# Flann
#------------------------------------------------------------------------------
if (BUILD3rd_Flann)
  message ("")
   message ("Add Flann to Build") 

  FetchContent_Declare(
    Flann
    GIT_REPOSITORY https://github.com/flann-lib/flann.git
    GIT_TAG        06a49513138009d19a1f4e0ace67fbff13270c69 # release 1.9.1

  )

  set (BUILD_TESTS            OFF)
  set (BUILD_DOC              OFF)
  set (BUILD_EXAMPLES         OFF)
  set (BUILD_MATLAB_BINDINGS  OFF)
  set (BUILD_PYTHON_BINDINGS  OFF)

  FetchContent_MakeAvailable(Flann)
   
  message ("Add Build Flann Finished")
  message ("")
endif (BUILD3rd_Flann)
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
  set (WITH_GSTREAMER      OFF)
  set (BUILD_EXAMPLES      OFF)
  set (BUILD_opencv_java   OFF)
  set (BUILD_opencv_python OFF)
  set (BUILD_opencv_hdf    OFF)  

  FetchContent_MakeAvailable(OpenCV)

  message ("Add Build OpenCV Finished")
  message ("")
endif (BUILD3rd_OpenCV)
#------------------------------------------------------------------------------


# CvPlot
#------------------------------------------------------------------------------
if (BUILD3rd_CvPlot)
  message ("")
  message("Downloading CvPlot")
 
  FetchContent_Declare(
    CvPlot
    GIT_REPOSITORY https://github.com/Profactor/cv-plot.git
    GIT_TAG        92ea307137e1abc3d49a5018ef80f4fbf189196b # release-1.2.2
  )
  message ("Downloading CvPlot Finished")

  message ("Add CvPlot to Build")
  set (CVPLOT_USE_CONAN OFF)  
  FetchContent_MakeAvailable(CvPlot)
  target_compile_options(CvPlot -DCVPLOT_USE_CONAN=OFF)  
  message ("Add Build CvPlot Finished")
  message ("")
endif (BUILD3rd_CvPlot)
#------------------------------------------------------------------------------

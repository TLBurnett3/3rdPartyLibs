cmake_minimum_required(VERSION 3.26)

project(3rdPartyLibs)

include(FetchContent)

if (WIN32)
set (CMAKE_INSTALL_PREFIX    /FoVI3D/3rdPartyLibs)
endif (WIN32)

set (CMAKE_DEBUG_POSTFIX d)


option(BUILD_GLM              "Build GLM"                 OFF)
option(BUILD_FlatBuffers      "Build FlatBuffers"         OFF)
option(BUILD_JSon             "Build nLohmann JSon"       OFF)
option(BUILD_ZMQ              "Build ZMQ"                 OFF)
option(BUILD_OpenCV           "Build OpenCV"              OFF)
option(BUILD_CvPlot           "Build CvPlot"              OFF)
option(BUILD_Eigen            "Build Eigen"               OFF)
option(BUILD_Flann            "Build Flann"               OFF)


# GLM
#------------------------------------------------------------------------------
if (BUILD_GLM)
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
endif (BUILD_GLM)
#------------------------------------------------------------------------------


# FlatBuffers
#------------------------------------------------------------------------------
if (BUILD_FlatBuffers)
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
endif (BUILD_FlatBuffers)
#------------------------------------------------------------------------------


# nLohmann JSon
#------------------------------------------------------------------------------
if (BUILD_JSon)
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
endif (BUILD_JSon)
#------------------------------------------------------------------------------


# ZMQ
#------------------------------------------------------------------------------
if (BUILD_ZMQ)
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
endif (BUILD_ZMQ)
#------------------------------------------------------------------------------


# Eigen
#------------------------------------------------------------------------------
if (BUILD_Eigen)
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
endif (BUILD_Eigen)
#------------------------------------------------------------------------------


# Flann
#------------------------------------------------------------------------------
if (BUILD_Flann)
  message ("")
  message("Downloading Flann")
  FetchContent_Declare(
    Flann
    GIT_REPOSITORY https://github.com/flann-lib/flann.git
  )
  FetchContent_MakeAvailable(Flann)
  message ("Downloading Flann Finished")
  message ("")
endif (BUILD_Flann)
#------------------------------------------------------------------------------


# OpenCV
#------------------------------------------------------------------------------
if (BUILD_OpenCV)
  message ("")
  message("Downloading OpenCV")
  set (WITH_GSTREAMER      OFF)
  set (BUILD_EXAMPLES      OFF)
  set (BUILD_opencv_java   OFF)
  set (BUILD_opencv_python OFF)
  set (BUILD_opencv_hdf    OFF)
  FetchContent_Declare(
    OpenCV
    GIT_REPOSITORY  https://github.com/opencv/opencv.git
    GIT_TAG         dad8af6b17f8e60d7b95a1203a1b4d22f56574cf # release 4.9.0
  )
  FetchContent_MakeAvailable(OpenCV)
  message ("Downloading OpenCV Finished")
  message ("")
endif (BUILD_OpenCV)
#------------------------------------------------------------------------------


# CvPlot
#------------------------------------------------------------------------------
if (BUILD_CvPlot)
  message ("")
  message("Downloading CvPlot")
  set (CVPLOT_USE_CONAN OFF)
  FetchContent_Declare(
    CvPlot
    GIT_REPOSITORY https://github.com/Profactor/cv-plot.git
    GIT_TAG        92ea307137e1abc3d49a5018ef80f4fbf189196b # release-1.2.2
  )
  FetchContent_MakeAvailable(CvPlot)
  message ("Downloading CvPlot Finished")
  message ("")
endif (BUILD_CvPlot)
#------------------------------------------------------------------------------

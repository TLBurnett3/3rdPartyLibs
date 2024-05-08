cmake_minimum_required(VERSION 3.26)

project(3rdPartyLibs)

include(FetchContent)
include(ExternalProject)

if (WIN32)
set (CMAKE_GENERATOR_PLATFORM   x64)
set (CMAKE_INSTALL_PREFIX       /3rdPartyLibs)
endif (WIN32)

set (CMAKE_DEBUG_POSTFIX      d)
set (CMAKE_CXX_STANDARD       17)

set (CMAKE_MODULE_PATH        ${CMAKE_INSTALL_PREFIX}
                              ${CMAKE_INSTALL_PREFIX}/cmake
                              ${CMAKE_INSTALL_PREFIX}/lib/cmake                              
                              ${CMAKE_INSTALL_PREFIX}/share
                              )

set (CMAKE_PREFIX_PATH        ${CMAKE_MODULE_PATH}
                              )
                              
set (ALLOW_DUPLICATE_CUSTOM_TARGETS OFF)

if (UNIX)
  set (CMAKE_C_COMPILER                      /usr/bin/gcc-8 CACHE PATH "" FORCE)
  set (CMAKE_CXX_COMPILER                    /usr/bin/g++-8 CACHE PATH "" FORCE)
  set (CMAKE_CXX_FLAGS_DEBUG                 "-g")
  set (CMAKE_CXX_FLAGS_RELEASE               "-O3")  
  set(CMAKE_POSITION_INDEPENDENT_CODE        ON)
endif (UNIX)


#------------------------------------------------------------------------------
# Options
# sudo make install InstallFlann InstallUSB
option(BUILD3rd_Group1           "Build Group 1 Libraries"   OFF)
option(BUILD3rd_Group2           "Build Group 2 Libraries"   OFF)
option(BUILD3rd_Group3           "Build Group 3 Libraries"   OFF)
option(BUILD3rd_Group4           "Build Group 4 Libraries"   OFF)
option(BUILD3rd_Group5           "Build Group 5 Libraries"   OFF)
option(BUILD3rd_Group6           "Build Group 6 Libraries"   OFF) 
option(BUILD3rd_Group7           "Build Group 7 Libraries"   OFF) 
option(BUILD3rd_Group8           "Build Group 8 Libraries"   OFF) 
option(BUILD3rd_Group9           "Build Group 9 Libraries"   OFF) 

# Group 1
option(BUILD3rd_zLib             "Build zLib"                OFF)     
option(BUILD3rd_GLM              "Build GLM"                 OFF)   
option(BUILD3rd_GLEW             "Build GLEW"                OFF)   
option(BUILD3rd_GLFW             "Build GLFW"                OFF)       
option(BUILD3rd_GLUT             "Build GLUT"                OFF)     
option(BUILD3rd_USB              "Build USB"                 OFF)   # make InstallUSB  
option(BUILD3rd_FreeType         "Build FreeType"            OFF)     
option(BUILD3rd_Sodium           "Build Sodium"              OFF)     
option(BUILD3rd_FlatBuffers      "Build FlatBuffers"         OFF)     
option(BUILD3rd_JSon             "Build nLohmann JSon"       OFF)     
option(BUILD3rd_ZMQ              "Build ZMQ"                 OFF)     
# Group 2
option(BUILD3rd_HDF5             "Build HDF5"                OFF)   # Needs to be build by itself
# Group 3
option(BUILD3rd_Flann            "Build Flann"               OFF)   # Needs to be build by itself
# Group 4
option(BUILD3rd_Eigen            "Build Eigen"               OFF)     
option(BUILD3rd_Boost            "Build Boost"               OFF)
# Group 5
option(BUILD3rd_SDL              "Build SDL"                 OFF) 
option(BUILD3rd_VTK              "Build VTK"                 OFF)     
# Group 6
option(BUILD3rd_OpenCV           "Build OpenCV"              OFF) 
option(BUILD3rd_CvPlot           "Build CvPlot"              OFF)       
option(BUILD3rd_Assimp           "Build Assimp"              OFF)     
# Group 7
option(BUILD3rd_PCL              "Build PCL"                 OFF)   # Windows build system hopelessly broken
# Group 8
option(BUILD3rd_RealSense        "Build RealSense"           OFF)   # uninstall target conflict 
# Group 9
option(BUILD3rd_Bullet           "Build Bullet"              OFF)    

# Group N - not really into building
option(BUILD3rd_CZMQ             "Build CZMQ"                OFF) 
option(BUILD3rd_VCPkg            "Build VCPkg"               OFF) 
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
  include(Inc/zLib.txt)
endif (BUILD3rd_Group1 OR BUILD3rd_zLIB)
#------------------------------------------------------------------------------


# GLM
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_GLM)
  include(Inc/GLM.txt)
endif (BUILD3rd_Group1 OR BUILD3rd_GLM)
#------------------------------------------------------------------------------


# GLEW
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_GLEW)
  include(Inc/GLEW.txt)
endif (BUILD3rd_Group1 OR BUILD3rd_GLEW)
#------------------------------------------------------------------------------


# GLFW
#------------------------------------------------------------------------------
if (BUILD3rd_Group1 OR BUILD3rd_GLFW)
  include(Inc/GLFW.txt)
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
  include(Inc/FreeType.txt)
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


# HDF5
#------------------------------------------------------------------------------
if (BUILD3rd_Group2 OR BUILD3rd_HDF5)
  include(Inc/HDF5.txt)
endif (BUILD3rd_Group2 OR BUILD3rd_HDF5)
#------------------------------------------------------------------------------


# Flann
#------------------------------------------------------------------------------
if (BUILD3rd_Group3 OR BUILD3rd_Flann)
  include(Inc/Flann.txt)
endif (BUILD3rd_Group3 OR BUILD3rd_Flann)
#------------------------------------------------------------------------------


# Eigen
#------------------------------------------------------------------------------
if (BUILD3rd_Group4 OR BUILD3rd_Eigen)
  include(Inc/Eigen.txt)
endif (BUILD3rd_Group4 OR BUILD3rd_Eigen)
#------------------------------------------------------------------------------


# Boost
#------------------------------------------------------------------------------
if (BUILD3rd_Group4 OR BUILD3rd_Boost)
  include(Inc/Boost.txt)
endif (BUILD3rd_Group4 OR BUILD3rd_Boost)
#------------------------------------------------------------------------------


# SDL
#------------------------------------------------------------------------------
if (BUILD3rd_Group5 OR BUILD3rd_SDL)
  include(Inc/SDL.txt)
endif (BUILD3rd_Group5 OR BUILD3rd_SDL)
#------------------------------------------------------------------------------


# VTK
#------------------------------------------------------------------------------
if (BUILD3rd_Group5 OR BUILD3rd_VTK)
  include(Inc/VTK.txt)
endif (BUILD3rd_Group5 OR BUILD3rd_VTK)
#------------------------------------------------------------------------------


# OpenCV
#------------------------------------------------------------------------------
if (BUILD3rd_Group6 OR BUILD3rd_OpenCV)
  include(Inc/OpenCV.txt)
endif (BUILD3rd_Group6 OR BUILD3rd_OpenCV)
#------------------------------------------------------------------------------


# CvPlot
#------------------------------------------------------------------------------
if (BUILD3rd_Group6 OR BUILD3rd_CvPlot)
  include(Inc/CvPlot.txt)
endif (BUILD3rd_Group6 OR BUILD3rd_CvPlot)
#------------------------------------------------------------------------------


# Assimp
#------------------------------------------------------------------------------
if (BUILD3rd_Group6 OR BUILD3rd_Assimp)
  include(Inc/Assimp.txt)
endif (BUILD3rd_Group6 OR BUILD3rd_Assimp)
#------------------------------------------------------------------------------


# PCL
#------------------------------------------------------------------------------
if (BUILD3rd_Group7 OR BUILD3rd_PCL)
  include(Inc/PCL.txt)
endif (BUILD3rd_Group7 OR BUILD3rd_PCL)
#------------------------------------------------------------------------------


# RealSense
#------------------------------------------------------------------------------
if (BUILD3rd_Group8 OR BUILD3rd_RealSense)
  include(Inc/RealSense.txt)
endif (BUILD3rd_Group8 OR BUILD3rd_RealSense)
#------------------------------------------------------------------------------


# Bullet
#------------------------------------------------------------------------------
if (BUILD3rd_Group9 OR BUILD3rd_Bullet)
  include(Inc/Bullet.txt)
endif (BUILD3rd_Group9 OR BUILD3rd_Bullet)
#------------------------------------------------------------------------------





# VCPkg
#------------------------------------------------------------------------------
if (BUILD3rd_GroupN OR BUILD3rd_VCPkg)
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
endif (BUILD3rd_GroupN OR BUILD3rd_VCPkg)
#------------------------------------------------------------------------------


# CZMQ
#------------------------------------------------------------------------------
if (BUILD3rd_GroupN OR BUILD3rd_CZMQ)
  include(Inc/CZMQ.txt)
endif (BUILD3rd_GroupN OR BUILD3rd_CZMQ)
#------------------------------------------------------------------------------


message ("")
message ("")

if (WIN32)
if (BUILD3rd_Group1 OR BUILD3rd_USB)
message ("To finish installing USB: make InstallUSB")
endif (BUILD3rd_Group1 OR BUILD3rd_USB)
endif (WIN32)

if (BUILD3rd_Group6 OR BUILD3rd_CvPlot)
  message ("To finish installing CvPlot: make InstallCvPlot")
endif (BUILD3rd_Group6 OR BUILD3rd_CvPlot)

message ("")
message ("")



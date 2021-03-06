cmake_minimum_required(VERSION 3.5)

project(vParticleFilterTracker_comb)
#project(vParticleFilterTracker_inclPar)
#project(vParticleFilterTracker_strPar)

if(NOT CMAKE_CONFIGURATION_TYPES)
    if(NOT CMAKE_BUILD_TYPE)
        message(STATUS "Setting build type to 'Release' as none was specified.")
        set_property(CACHE CMAKE_BUILD_TYPE PROPERTY VALUE "Release")
    endif()
endif()

include(GNUInstallDirs)
find_package(YCM REQUIRED)
include(AddInstallRPATHSupport)
add_install_rpath_support(BIN_DIRS "${CMAKE_INSTALL_FULL_BINDIR}"
                          LIB_DIRS "${CMAKE_INSTALL_FULL_LIBDIR}"
                          INSTALL_NAME_DIR "${CMAKE_INSTALL_FULL_LIBDIR}"
                          USE_LINK_PATH)



find_package(YARP COMPONENTS os sig REQUIRED)
find_package(event-driven REQUIRED)

include_directories(${PROJECT_SOURCE_DIR}/include)

add_executable(${PROJECT_NAME} src/vControlLoopDelay_comb.cpp src/vParticle_comb.cpp
    include/vControlLoopDelay_comb.h include/vParticle_comb.h)
#add_executable(${PROJECT_NAME} src/vControlLoopDelay_strPar.cpp src/vParticle_strPar.cpp
#    include/vControlLoopDelay_strPar.h include/vParticle_strPar.h)

target_link_libraries(${PROJECT_NAME} PRIVATE YARP::YARP_os
                                              YARP::YARP_init
                                              ev::event-driven)

install(TARGETS ${PROJECT_NAME} DESTINATION ${CMAKE_INSTALL_BINDIR})

yarp_install(FILES ${PROJECT_NAME}.ini
             DESTINATION ${EVENT-DRIVEN_CONTEXTS_INSTALL_DIR}/event-driven)

option(ADD_DOCS_TO_IDE "Explicitly add apps/drivers to project IDE" OFF)
if(ADD_DOCS_TO_IDE)
    add_custom_target(${PROJECT_NAME}_docs SOURCES ${PROJECT_NAME}.ini)
endif(ADD_DOCS_TO_IDE)

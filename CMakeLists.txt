cmake_minimum_required(VERSION 3.0.0)

project(radioroom VERSION 2.1.0)

set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/bin)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

set(CPACK_GENERATOR "DEB")
set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "armhf")
set(CPACK_PACKAGE_NAME "radioroom")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Pavel Bobov")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Iridium SBD telemetry for MAVLink autopilots")
set(CPACK_PACKAGE_VENDOR "Envirover")
set(CPACK_PACKAGE_DESCRIPTION_FILE "${CMAKE_CURRENT_SOURCE_DIR}/README.md")
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/LICENSE")
set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -std=c++11" )

configure_file("${PROJECT_SOURCE_DIR}/src/build.h.in" "${PROJECT_BINARY_DIR}/build.h")

include_directories("${PROJECT_SOURCE_DIR}/libs/mavlink/include/standard")
include_directories("${PROJECT_BINARY_DIR}")

file(GLOB sources src/*.c src/*.cc)

add_executable(radioroom ${sources})

install(TARGETS radioroom DESTINATION "/usr/sbin")
install(DIRECTORY "${PROJECT_SOURCE_DIR}/etc/" DESTINATION "/etc" FILE_PERMISSIONS  )

include(CPack)

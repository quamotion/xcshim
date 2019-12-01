cmake_minimum_required(VERSION 3.10)

project(xcshim VERSION 0.1.2)

set(PACKAGE_AUTHOR "Quamotion bvba")

add_subdirectory(src)

SET(CPACK_GENERATOR "DEB")
SET(CPACK_DEBIAN_PACKAGE_DESCRIPTION "Run Appium tests on iOS devices, on Linux")
SET(CPACK_DEBIAN_PACKAGE_MAINTAINER "Frederik Carlier <frederik.carlier@quamotion.mobi>")
SET(CPACK_DEBIAN_PACKAGE_HOMEPAGE "http://docs.quamotion.mobi")
SET(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "all")
SET(CPACK_DEBIAN_PACKAGE_DEPENDS "xcuitrunner (>= 0.127.81), ios-deploy (>= 0.127.81)")
SET(CPACK_PACKAGE_FILE_NAME "${PROJECT_NAME}-${PROJECT_VERSION}")
INCLUDE(CPack)

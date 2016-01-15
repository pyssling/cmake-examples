cmake_minimum_required (VERSION 2.6)
project (Tutorial)
add_executable(Tutorial tutorial.cxx)

# The version number.
set (Tutorial_VERSION_MAJOR 1)
set (Tutorial_VERSION_MINOR 0)

install(TARGETS Tutorial
  DESTINATION bin
  COMPONENT NORMAL)

install(TARGETS Tutorial
  DESTINATION bin
  COMPONENT EXTRAS)

# build a CPack driven installer package
set (CPACK_PACKAGE_VERSION_MAJOR "${Tutorial_VERSION_MAJOR}")
set (CPACK_PACKAGE_VERSION_MINOR "${Tutorial_VERSION_MINOR}")


set (CPACK_GENERATOR "RPM")


set (CPACK_RPM_COMPONENT_INSTALL "ON")

set (CPACK_RPM_PACKAGE_NAME tutorial)
set (CPACK_RPM_PACKAGE_SUMMARY "tutorial for cmake, packaged!")

set (CPACK_RPM_PACKAGE_VERSION "${Tutorial_VERSION_MAJOR}.${Tutorial_VERSION_MINOR}")


set (CPACK_RPM_EXTRAS_PACKAGE_NAME tutorial-extras)
set (CPACK_RPM_EXTRAS_PACKAGE_SUMMARY "tutorial for cmake extras, packaged!")

set (CPACK_RPM_PACKAGE_VERSION "${Tutorial_VERSION_MAJOR}.${Tutorial_VERSION_MINOR}")


include (CPack)

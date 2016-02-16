cmake_minimum_required (VERSION 2.6)

# RPM generator
set (CPACK_GENERATOR "RPM")

set (CPACK_RPM_COMPONENT_INSTALL "ON")

# Tutorial Project
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

# Main package
set (CPACK_RPM_PACKAGE_NAME tutorial)
set (CPACK_RPM_PACKAGE_SUMMARY "tutorial for cmake, packaged!")
set (CPACK_RPM_PACKAGE_VERSION "${Tutorial_VERSION_MAJOR}.${Tutorial_VERSION_MINOR}")


# Extras Component
set (CPACK_RPM_EXTRAS_PACKAGE_NAME tutorial-extras)
set (CPACK_RPM_EXTRAS_PACKAGE_SUMMARY "tutorial for cmake extras, packaged!")
set (CPACK_RPM_PACKAGE_VERSION "${Tutorial_VERSION_MAJOR}.${Tutorial_VERSION_MINOR}")

# forbar Project

add_executable(forbar tutorial.cxx)

install(TARGETS forbar
  DESTINATION bin
  COMPONENT foo)

# build a CPack driven installer package
set (CPACK_PACKAGE_VERSION_MAJOR "${Tutorial_VERSION_MAJOR}")
set (CPACK_PACKAGE_VERSION_MINOR "${Tutorial_VERSION_MINOR}")


# Function for generating more RPMs
function(create_rpm component name description)
  project (forbar)
  set (CPACK_RPM_${component}_PACKAGE_NAME ${name})
  set (CPACK_RPM_${component}_PACKAGE_SUMMARY ${description})
  set (CPACK_RPM_${component}_VERSION "${Tutorial_VERSION_MAJOR}.${Tutorial_VERSION_MINOR}")
endfunction(create_rpm)

create_rpm("foo" "forbar-foo" "The foo packaged!")

include (CPack)

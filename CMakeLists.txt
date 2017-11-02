cmake_minimum_required()

project("QuantLib")
# to reference headers via <ql/foo.hpp>, we need to add the root
# directory of the project to includes
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

find_package(Boost)
if (Boost_FOUND)
  include_directories(${Boost_INCLUDE_DIRS})
endif (Boost_FOUND)

cmake_policy(SET CMP0042 NEW)

# Switch off the type conversion warning in Clang. Note: the warning should be fixed in the code.
#if (CMAKE_C_COMPILER_ID STREQUAL "Clang")
    set( CMAKE_CXX_FLAGS  "-Wno-conversion" )
#endif()
add_compile_options(-Wno-conversion)
message(STATUS, "CXXFLAGS: ${CMAKE_CXX_FLAGS}")
add_subdirectory(Examples)
add_subdirectory(ql)

# Building the test suite might require using shared libraries
# for Boost.Test
option(USE_BOOST_DYNAMIC_LIBRARIES
       "Use the shared version of Boost.Test" ON)
add_subdirectory(test-suite)


#CMAKE_XCODE_GENERATE_SCHEME = true

cmake_minimum_required(VERSION 3.10)

# Set the project name
project(Tutorial VERSION 1.0)

option(USE_MYMATH "Use tutorial provided math implementation" ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Can't be placed before the line6, because the definition is depending on the option
configure_file(TutorialConfig.h.in TutorialConfig.h)

if(USE_MYMATH)
  add_subdirectory(MathFunctions)
  # The following line is not needed after we use INTERFACE in lib CMakeLists
  # list(APPEND EXTRA_LIBS MathFunctions) 
  list(APPEND EXTRA_INCLUDES "${PROJECT_SOURCE_DIR}/MathFunctions")
endif()

# Add the executable
add_executable(Tutorial tutorial.cxx)

target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

target_include_directories(Tutorial PUBLIC 
                           "${PROJECT_BINARY_DIR}"
                           # The following line is not needed after we use INTERFACE in lib CMakeList
                           # "${EXTRA_INCLUDES}"
                           )
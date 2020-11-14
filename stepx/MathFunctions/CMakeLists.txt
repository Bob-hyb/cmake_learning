add_library(MathFunctions mysqrt.cxx)

# Does this system provide the log and exp functions?
include(CheckSymbolExists)
check_symbol_exists(log "math.h" HAVE_LOG)
check_symbol_exists(exp "math.h" HAVE_EXP)
# If log and exp are not initially found, require the m library and try again.
if (NOT (HAVE_LOG AND HAVE_EXP))
  unset(HAVE_LOG CACHE)
  unset(HAVE_EXP CACHE)
  set(CMAKE_REQUIRED_LIBRARIES "m")
  check_symbol_exists(log "math.h" HAVE_LOG)
  check_symbol_exists(exp "math.h" HAVE_EXP)
  if (HAVE_LOG AND HAVE_EXP)
    target_link_libraries(MathFunctions PRIVATE m)
  endif()
endif()

# INTERFACE means things that consumers require but the producer doesn’t.
# So if we include the source directory of a library in our project directory,
# we don't need to add the source directory to our project's include path explicitly,
# all we need to do is to link the library and the source directory will be automatically
# added to our project directory.
target_include_directories(MathFunctions
                           INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
                           PRIVATE ${CMAKE_BINARY_DIR})                               

install(TARGETS MathFunctions DESTINATION /home/ybhuang/torment/cmake_learning/cmake_learning/install)
install(FILES MathFunctions.h DESTINATION /home/ybhuang/torment/cmake_learning/cmake_learning/install)
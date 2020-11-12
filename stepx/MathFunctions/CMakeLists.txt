add_library(MathFunctions mysqrt.cxx)

# INTERFACE means things that consumers require but the producer doesn’t.
# So if we include the source directory of a library in our project directory,
# we don't need to add the source directory to our project's include path explicitly,
# all we need to do is to link the library and the source directory will be automatically
# added to our project directory.
target_include_directories(MathFunctions
                           INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})                               
set(libsrc procstat.c percentile.c)

add_library(objlib OBJECT ${libsrc})
set_property(TARGET objlib PROPERTY POSITION_INDEPENDENT_CODE ON)


add_library(procstat_shared SHARED $<TARGET_OBJECTS:objlib>)
SET_TARGET_PROPERTIES(procstat_shared PROPERTIES OUTPUT_NAME procstat CLEAN_DIRECT_OUTPUT 1)

add_library(procstat_static STATIC $<TARGET_OBJECTS:objlib>)
SET_TARGET_PROPERTIES(procstat_static PROPERTIES OUTPUT_NAME procstat CLEAN_DIRECT_OUTPUT 1)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -D_FILE_OFFSET_BITS=64 -g")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -O0 -ggdb")


install (TARGETS procstat_shared
         ARCHIVE DESTINATION lib
         LIBRARY DESTINATION lib
         RUNTIME DESTINATION bin)

install (TARGETS procstat_static
         ARCHIVE DESTINATION lib
         LIBRARY DESTINATION lib
         RUNTIME DESTINATION bin)

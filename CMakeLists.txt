# Defines softfloat library
project (SoftFloat )

# generate compile command database for external tools
set (CMAKE_EXPORT_COMPILE_COMMANDS "ON")

message ( STATUS "Configuring SoftFloat" )
set( C_DEFINES "-DSOFTFLOAT_ROUND_EVEN -DINLINE_LEVEL=5 -DSOFTFLOAT_FAST_DIV32TO16 -DSOFTFLOAT_FAST_DIV64TO32 -DSOFTFLOAT_FAST_INT64" )
set( CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror-implicit-function-declaration -Wno-conversion ${C_DEFINES}" )

file ( GLOB HEADERS "source/include/*.h" "build/Linux-x86_64-GCC" "source/8086-SSE" )
file ( GLOB SOURCES "source/*.c" )
add_library ( softfloat ${SOURCES} ${HEADERS} )
target_include_directories( softfloat PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/source/include" "${CMAKE_CURRENT_SOURCE_DIR}/source/8086-SSE" "${CMAKE_CURRENT_SOURCE_DIR}/build/Linux-x86_64-GCC" )

install ( TARGETS
   softfloat

   RUNTIME DESTINATION bin
   LIBRARY DESTINATION lib
   ARCHIVE DESTINATION lib
)

#install ( FILES ${HEADERS} DESTINATION "include/" )

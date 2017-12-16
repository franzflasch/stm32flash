project (stm32flash)
cmake_minimum_required(VERSION 2.8)

### Common Settings
set(CMAKE_BUILD_TYPE Release)
#set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror")
set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -Wall -Werror")

### parsers
include_directories(parsers)
set(PARSER_SRCS parsers/binary.c parsers/hex.c)

### executable
include_directories(.)
set(EXEC_SRCS dev_table.c
			  i2c.c
			  init.c
			  main.c
			  port.c
			  serial_common.c
			  serial_platform.c
			  stm32.c
	          utils.c)

add_executable(stm32flash ${PARSER_SRCS} ${EXEC_SRCS})
install(TARGETS stm32flash RUNTIME DESTINATION bin)

### Debian Package generation
set(CPACK_GENERATOR "DEB")
set(CPACK_PACKAGE_VERSION "0.1.0")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Franz Flasch")
include(CPack)

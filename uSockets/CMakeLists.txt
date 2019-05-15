cmake_minimum_required(VERSION 3.10)
PROJECT(uSockets)

FILE(GLOB C_FILES src/eventing/*.c src/*.c)

INCLUDE_DIRECTORIES(src)

SET(CMAKE_C_FLAGS "-std=c11 -DLIBUS_NO_SSL -DLIBUS_USE_LIBUV")

ADD_LIBRARY(usockets SHARED ${C_FILES})

TARGET_LINK_LIBRARIES(usockets uv)

ADD_EXECUTABLE(echo_server examples/echo_server.c ${C_FILES})

ADD_EXECUTABLE(http_server examples/http_server.c ${C_FILES})

TARGET_LINK_LIBRARIES(echo_server uv)
TARGET_LINK_LIBRARIES(http_server uv)

INSTALL(TARGETS usockets DESTINATION /usr/local/lib)
INSTALL(DIRECTORY include DESTINATION /usr/local)


